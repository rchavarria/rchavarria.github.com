---
title: "[microtip] git: ramas locales y remotas"
date: 2012-11-19 11:19
author: Rubén Chavarría
categories: 
- git
- microtip
- software
comments: true
published: true
footer: false
sidebar: true
---

[`git`](http://es.wikipedia.org/wiki/Git) es un sistema de control de version 
distribuido 
([DVCS](http://en.wikipedia.org/wiki/Distributed_version_control_system) por 
sus siglas en inglés), y una de sus características que lo hacen más atractivo 
es su gran rapidez para trabajar con ramas (*branches*).


En este pequeño post, que he llamado <strong>microtip</strong>, veremos cómo 
crear una rama, movernos entre ramas, realizar sencillos *merge* 
entre ramas y cómo hacer que estos cambios se vean reflejados en un repositorio 
remoto para poder compartirlo con nuestros compañeros de proyecto.

<!-- more -->

Para comenzar a trabajar en una rama nueva, podemos hacerlo de dos formas:

- Crear la rama y movernos a ella

```
git branch nueva_rama
git checkout nueva_rama
```

- Movernos a una rama y crearla en caso de que no exista

```
git checkout -b nueva_rama
```

Ok, ya estamos trabajando en la nueva rama. Ahora podemos añadir ficheros, 
hacer commit de cambios que hayamos hecho, ...

```
git add nuevo_fichero.txt
git commit -m "mensaje para el commit"
```

Una vez tenemos los cambios deseados en nuestra rama, podemos dejarlo así, de 
forma que será una rama privada, solamente nosotros tendremos acceso a ella, o 
podremos hacerla pública a través de algún repositorio remoto para que sea 
accesible por nuestros compañeros:

```
git push origin new_branch
```

Nota: este comando supone que *origin* es un remote válido para git.

Si queremos pasar estos cambios otra rama, por ejemplo, master: primero nos 
moveremos a esa rama y luego traemos los cambios a esta rama:

```
git checkout master
git merge development master
```
