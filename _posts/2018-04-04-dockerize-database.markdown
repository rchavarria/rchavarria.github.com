---
layout: post
title: "Dockerizar una base de datos"
date: 2018-04-04 00:00
author: Ruben Chavarria
categories:
- Proyectos
- Docker
---

Llevo entre manos un proyecto software, da un poco igual de qué se trata. Pero como
casi todo software, necesita guardar datos, y la idea es guardarlos en una base de
datos.

¿Qué base de datos utilizar? En un principio había pensado en
[PostgreSQL](https://www.postgresql.org/), por ser software libre, pero no tengo
nada de experiencia con ella. Sí estoy acostumbrado a MySQL, pero prefiero usar
software libre, así que me voy a decidir por [MariaDB](https://mariadb.org/),
que es prácticamente un MySQL, pero en software libre.

<!-- more -->

Las primeras pruebas las hice con PostgreSQL, y fueron muy fáciles. Las siguientes
las hice con MariaDB, y fueron igual de fáciles. Así que aquí cuento cómo usar
una imagen de docker de MariaDB para tener la base de datos funcionando.

## Obtener la imagen docker

He usado la imagen la [última imagen de `mariadb`](https://hub.docker.com/_/mariadb/)

## Arrancar un contendor de dicha imagen

En la misma documentación de la imagen indican cómo arrancar un contenedor, pero para
ahorrar tiempo, el comando sería tal que así:

```
docker run \
    -p 3306:3306 \
    --env MYSQL_ROOT_PASSWORD=root-pwd \
    --env MYSQL_USER=user \
    --env MYSQL_PASSWORD=password \
    --env MYSQL_DATABASE=db \
    --name mariadb-db \
    -d \
    mariadb:latest 
```

- `-p 3306:3306`: para publicar el puerto `3306` y que sea accesible desde fuera
del contenedor
- `-d`: para que el contenedor se quede ejecutando como un *demonio*
- `--env MYSQL_ROOT_PASSWORD=root-pwd`: configurar la contraseña del usuario `root`
de la base de datos
- `--env MYSQL_USER=user`: configurar el nombre del usuario a crear
- `--env MYSQL_PASSWORD=password`: configurar la contraseña del usuario `user`
- `--env MYSQL_DATABASE=db`: nombre de la base de datos a crear. El usuario `user`
tendrá acceso completo a esta base de datos

## Conectar al contendor creado

De entre los muchos clientes para acceder a MariaDB (o MySQL), he escogido con el que
viene integrado en el IDE PhpStorm, que es el IDE al que estoy acostumbrado. También
podría haber elegido phpMyAdmin, o algún otro gestor de bases de datos gráfico.

En PhpStorm, crear un nuevo datasource, de tipo MySQL (funciona bien para MariaDB
supongo), y configurar host, puerto, base de datos, usuario y contraseña. Lo básico
vamos:

![some image](/notes/assets/images/2018/phpstorm-mysql-datasource.png)
