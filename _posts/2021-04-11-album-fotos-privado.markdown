---
layout: post
title: "Álbum de fotos online, privado"
date: 2021-04-11 18:30
author: Ruben Chavarria
categories:
- Fotos
- Proyectos
---

Aquí intento describir cómo he montado un servicio de álbum de fotos online, pero privado,
donde yo gestiono el hardware y el software, aunque de software no he creado nada en este proyecto.
Uno nombre más llamativo podría ser *Google Photos privado*

La idea surge de los servicios *auto hospedados*. Existe un [sin fin de estos servicios][1]: desde
álbumes de fotos hasta editores de código online.

El proyecto que tengo en la cabeza es el siguiente:

> Hospedar en una Raspberry PI un software que me permita catalogar y comentar mis fotos personales,
> así, cuando vengan amigos a casa, poder compartirlos con ellos a través de la red privada de casa.
> Si todo va bien, podría exponer el servicio a través de internet, para poder compartirlas con más
> amigos

<-- more -->

## Comenzando

Comenzamos con la lista de posibles servicios en el repositorio de GitHub [awesome-selfhosted][1]:

- Uno: blah blah
- Dos: blah foo
- Tres....

Uno muy interesante para el proyecto que tengo en mente es [PhotoPrism][2], y tiene la opción de
montarse en Docker, en una [Raspberry PI][3], así que es por donde voy a comenzar.

Una de los primeros requisitos que tiene es que la arquitectura de la Raspberry tiene que ser
ARM 64 bits, por lo que hay que cambiar `config.txt` en la misma y poner `arm64bit=1`.

Por lo pronto, necesito actualizar mi Raspberry. Actualizo a la distribución Raspberry OS,
antiguamente conocida como *Raspbian*

## Instalar Raspberry 64 bits

No he encontrado ninguna referencia a cambiar la arquitectura del sistema operativo
de la Raspberry *en caliente*. Creo que va a tocar instalar un nuevo sistema
operativo desde 0 en ella.

Para ello, hay que grabar una imagen en una tarjeta de memoria. Parece que,
oficialmente, solo existen versiones de 32 bits. La versión de 64 bits es bastante
moderna, y no está todavía estable.

Se puede conseguir en el centro de descargas de Raspberry PI,
[Raspberry OS 64 bit][4], y se puede grabar en la tarjeta de memoria usando
[Raspberry Pi Imager][5].

Para comprobar la arquitectura del sistema, se puede comprobar con el comando
`uname`

```
$ uname -a
Linux raspberrypi 5.10.17-v8+ #1421 SMP PREEMPT Thu May 27 14:01:37 BST 2021 aarch64 GNU/Linux
```

## Instalar docker y docker-compose

La manera más sencilla y menos problemática para instalar `docker` en una Raspberry
parece ser usando un [script proporcionado por Docker][6]:

```
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
```

Y para `docker-compose`:

```
$ sudo apt install libffi-dev libssl-dev python3-dev python3 python3-pip
$ sudo pip3 install docker-compose
```

## Ejecutar el fichero de despliegue de PhotoPrism

De la documentación oficial de PhotoPrism, para *instalarlo* en la Raspberry,
debemos descargar un fichero `docker-compose.yml` y levantar los servicios que
se definen en él:

```
$ wget https://dl.photoprism.org/docker/arm64/docker-compose.yml
$ sudo docker-compose up -d
...
Creating mariadb    ... done
Creating photoprism ... done
```

¡Arrancado!

A partir de aquí, podemos echar un vistazo a la documentación para saber
[qué podemos hacer con `docker-compose`][7]:

- Visitar `http://localhost:2342` en el navegador para comenzar a usarlo
- `docker-compose stop`: para parar el servicio
- `docker-compose logs --tail=25 -f` para ver los logs
- Documentación sobre los [comandos disponibles][8]

## Usando PhotoPrism

Entrar a la web de PhotoPrism, a través de [http://localhost:2342], hacer login
como `admin` (la contraseña está en el fichero `.yml` que hemos arrancado)

Ahora podemos importar nuestras fotos, subirlas y jugar con ellas

## Problema: se cuelga al indexar las fotos

Para poder mostar resultados, PhotoPrism debe indexarlas. Pero al subir solamente
una, para probar, se queda colgado. Es como que se queda sin memoria, la
Raspberry necesita más potencia, o no sé qué...

Tarda 2000 seg en indexar 4 fotos, ¡4! Puede que tenga un problema de memoria.
Parece que la Raspberry no tiene partición de swap, veamos si se puede hacer
algo con eso

Ok, no tiene partición, pero sí usa un fichero de swap, y [se puede configurar][9]

Hay que modificar el fichero `/etc/dphys-swapfile` y reiniciar claro

En varios artículos mencionan que no es buena idea tener un fichero de swap en
la tarjeta de memoria de la Raspberry, que es muy lenta. Claro que algunos 
recomiendan incluso un disco duro mecánico, así que no sé qué creer

En ese fichero, el swap tiene 100Mb configurados. Voy a probar con 1Gb, lo mismo
que la memoria RAM

## Deshabilitar funcionalidades

Para intentar hacer que PhotoPrism use menos CPU y memoria, deshabilito algunas
de las funcionalidades. Puede que éstas sean muy interesantes, pero estoy seguro
de que consumen muchos recursos, y la Raspberry no está sobrada de ellos.

En el fichero `docker-compose.yml` proporcionado, modifico valores:

- `PHOTOPRISM_DEBUG`
- `PHOTOPRISM_EXPERIMENTAL`
- `PHOTOPRISM_DISABLE_WEBDAV`
- `PHOTOPRISM_DISABLE_TENSORFLOW`
- `PHOTOPRISM_DETECT_NSFW`
- `PHOTOPRISM_UPLOAD_NSFW`

## Disco duro externo

Ok, ya tenemos PhotoPrism ejecutándose y funcionando.

Una primera prueba subiendo unas pocas fotos a través de la interfaz web de la
herramienta y parece que funciona

Pero claro, el almacenamiento de la Raspberry es bastante limitado, y la mayoría
de las fotos las tengo en un disco duro externo

Estos son los comandos para montar y desmontar unidades en Linux:

```bash
$ lsblk
$ sudo mount /dev/sda1 /mnt/external-disk
$ sudo umount /dev/sda1
```

La idea general es montar el disco duro en la Raspberry, configurar el fichero
`docker-compose.yml` de PhotoPrism para enlazar los volúmenes de los contendores
usados a los directorios adecuados del disco duro externo. Y, por fin, arrancar
PhotoPrism y a disfrutar

## Guía rápida de los comandos usados

```bash
# listar los dispositivos de bloque para encontrar el disco externo
$ lsblk

# montar disco duro
$ sudo mount /dev/sda1 /mnt/external-disk

# editar configuración PhotoPrism
$ cd ~/photoprism
$ vi docker-compose.yml

# arrancar PhotoPrism
$ docker-compose up -d

# ver logs de las herramientas
$ docker-compose logs --tail=30 -f

# parar PhotoPrism
$ docker-compose stop

# desmontar disco
$ sudo umount /dev/sda1
```

[1]: https://github.com/awesome-selfhosted/awesome-selfhosted
[2]: https://docs.photoprism.org/
[3]: https://docs.photoprism.org/getting-started/raspberry-pi/
[4]: https://downloads.raspberrypi.org/raspios_arm64/images/raspios_arm64-2021-04-09/2021-03-04-raspios-buster-arm64.zip
[5]: https://www.raspberrypi.org/software/
[6]: https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script
[7]: https://docs.photoprism.org/getting-started/docker-compose/
[8]: https://docs.photoprism.org/getting-started/docker-compose/#command-reference
[9]: http://raspberrypimaker.com/adding-swap-to-the-raspberrypi/
