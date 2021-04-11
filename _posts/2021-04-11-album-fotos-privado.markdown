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

[1]: https://github.com/awesome-selfhosted/awesome-selfhosted
[2]: https://docs.photoprism.org/
[3]: https://docs.photoprism.org/getting-started/raspberry-pi/