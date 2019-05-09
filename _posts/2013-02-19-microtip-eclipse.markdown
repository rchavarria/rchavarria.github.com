---
title: "[microtip] eclipse: Detail Formatters"
date: 2013-02-19 17:19
author: Rubén Chavarría
comments: true
categories: 
- microtip
- ide
- eclipse
published: true
footer: false
sidebar: true
---

A través del post de [Kinisoftware](http://twitter.com/kinisoftware): 
[A la caza del bug en eclipse](http://kinisoftware.com/2013/02/a-la-caza-del-bug-en-eclipse/)
me encontré con un link muy recomendable, si trabajas con Eclipse como IDE:
[Effective Java debugging with Eclipse](http://eclipsesource.com/blogs/2013/01/08/effective-java-debugging-with-eclipse/).

En ese link aparecen multitud de consejos sobre cómo hacer debug en eclipse de una manera
mucho más productiva. Entre estos consejos están los *Detail Formatters*, para formatear
de una forma mucho más avanzada que con un simple `toString()` aquellas clases que desees.

<!-- more -->

En un primer momento, me parecieron muy útiles, pero no profundicé en ellos. Pensé que 
cada vez que iniciara la depuración de una aplicación, debía crearme los Detail
Formatters que deseaba, y me pareció muy laborioso.

Pero no es así, estos formatters se guardan en tus preferencias, y los puedes
editar siempre que quieras. Los encontrarás en el menú `Window` > `Preferences`.
Y dentro de preferencias, en `Java` > `Debug` > `Detail Formatters`.

## Buscando una excusa

Una vez que me convencí de su utilidad, había que crear alguno, ¿no?. Actualmente
me encuentro con que trabajo bastante con el tipo de Java `java.awt.geom.Rectangle2D`,
y la verdad es que no me gusta nada cómo Eclipse me muestra este tipo de datos
en una sesión de debugging.

![Rectangle2D sin detail formatter]({{ site.baseurl }}/assets/images/2013/rectangle2d-without-detail-formatter.png)

## Crear un detail formatter

Manos a la obra. Primero, establecemos un punto de ruptura donde podamos ver en la vista
*Variables* una variable de la clase deseada, en este caso de `java.awt.geom.Rectangle2D`.

Pinchamos con el botón derecho del ratón y seleccionamos la opción *New Detail Formatter...*.

Ahora tenemos a nuestra disposición una ventana donde podemos introducir código Java de forma
que retorne una `String` con la representación que nosotros queramos. Yo he usado el siguiente
código:

``` java
java.text.NumberFormat nf = 
    java.text.NumberFormat.getInstance(java.util.Locale.ENGLISH);
nf.setMaximumFractionDigits(2);
nf.setGroupingUsed(false);

return 
    "x: " + nf.format(getX()) + "\n" +
    "y: " + nf.format(getY()) + "\n" +
    "w: " + nf.format(getWidth()) + "\n" +
    "h: " + nf.format(getHeight());
```

Y éste es el resultado, para mi gusto, mucho más compacto y directo:

![Rectangle2D usando detail formatter]({{ site.baseurl }}/assets/images/2013/rectangle2d-using-detail-formatter.png)

## Conclusión

En cualquier proyecto nos podemos encontrar con clases que no podremos modificar (frameworks, 
librerías, código legacy, ...). Pero no nos tenemos que conformar con sus tristes y aburridos
métodos `toString()`. Podemos escribir nuestro propio código para formatear estos tipos de datos.
Y lo mejor de todo, podemos reutilizarlo, ya que nuestros formatters se guardan como preferencias
de nuestro IDE favorito.
