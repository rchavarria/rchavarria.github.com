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

Comenzamos con la lista de posibles servicios en el repositorio de GitHug [awesome-selfhosted][1]:

- Uno: blah blah
- Dos: blah foo
- Tres....

Uno muy interesante para el proyecto que tengo en mente es [PhotoPrism][2], y tiene la opción de
montarse en Docker, en una [Raspberry PI][3], así que es por donde voy a comenzar.

Una de los primeros requisitos que tiene es que la arquitectura de la Raspberry tiene que ser
ARM 64 bits, por lo que hay que cambiar `config.txt` en la misma y poner `arm64bit=1`.

Por lo pronto, necesito actualizar mi Raspberry. Actualizo a la distribución Raspberry OS,
antiguamente conocida como *Raspbian*

No he encontrado ninguna referencia a cambiar la arquitectura del sistema operativo
de la Raspberry *en caliente*. Creo que va a tocar instalar un nuevo sistema
operativo desde 0 en ella.

Para ello, hay que grabar una imagen en una tarjeta de memoria. Parece que,
oficialmente, solo existen versiones de 32 bits. La versión de 64 bits es bastante
moderna, y no está todavía estable.

Se puede conseguir en el centro de descargas de Raspberry PI,
[Raspberry OS 64 bit][4], y se puede grabar en la tarjeta de memoria usando
[Raspberry Pi Imager][5].

Continuará...

[1]: https://github.com/awesome-selfhosted/awesome-selfhosted
[2]: https://docs.photoprism.org/
[3]: https://docs.photoprism.org/getting-started/raspberry-pi/
[4]: https://downloads.raspberrypi.org/raspios_arm64/images/raspios_arm64-2021-04-09/2021-03-04-raspios-buster-arm64.zip
[5]: https://www.raspberrypi.org/software/
