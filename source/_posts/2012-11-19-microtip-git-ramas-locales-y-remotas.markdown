
---
layout: page
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

<p><a href="http://es.wikipedia.org/wiki/Git"><strong>git</strong></a> es un sistema de control de version distribuido (<a href="http://en.wikipedia.org/wiki/Distributed_version_control_system">DVCS</a> por sus siglas en inglés), y una de sus características que lo hacen más atractivo es su gran rapidez para trabajar con ramas (<em>branches</em>).</p>

<p>En este pequeño post, que he llamado <strong>microtip</strong>, veremos cómo crear una rama, movernos entre ramas, realizar sencillos <em>merge</em> entre ramas y cómo hacer que estos cambios se vean reflejados en un repositorio remoto para poder compartirlo con nuestros compañeros de proyecto.</p>

<!-- more -->

<p>Para comenzar a trabajar en una rama nueva, podemos hacerlo de dos formas:
<ol>
	<li>Crear la rama y movernos a ella</li>
```
git branch nueva_rama
git checkout nueva_rama
```
	<li>Movernos a una rama y crearla en caso de que no exista</li>
```
git checkout -b nueva_rama
```
</ol>
</p>

<p>Ok, ya estamos trabajando en la nueva rama. Ahora podemos añadir ficheros, hacer commit de cambios que hayamos hecho, ...</p>

```
git add nuevo_fichero.txt
git commit -m &quot;mensaje para el commit&quot;
```

<p>Una vez tenemos los cambios deseados en nuestra rama, podemos dejarlo así, de forma que será una rama privada, solamente nosotros tendremos acceso a ella, o podremos hacerla pública a través de algún repositorio remoto para que sea accesible por nuestros compañeros:</p>

```
git push origin new_branch
```

<p style="font-size:75%;text-align:right;">Nota: este comando supone que <em>origin</em> es un remote válido para git.</p>

<p>Si queremos pasar estos cambios otra rama, por ejemplo, master: primero nos moveremos a esa rama y luego traemos los cambios a esta rama:</p>

```
git checkout master
git merge development master
```
