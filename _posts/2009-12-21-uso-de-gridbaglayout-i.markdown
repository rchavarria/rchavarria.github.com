---
title: "Uso de GridBagLayout (I)"
date: 2009-12-21 22:01
author: Rubén Chavarría
categories: 
- java
- swing
- gridbaglayout
- swing layout manager
comments: true
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
  <p>Este post pertenece a mi antiguo blog en <a href="http://rchavarria.wordpress.com">wordpress</a>, pero decidí pasarme a github:pages por las siguientes <a href="/blog/2012/12/03/por-que-cambie-mi-blog-en-wordpress-com">razones</a></p>
</div>

En esta entrada veremos el uso básico de `GridBagLayout`, si se desea profundizar 
más en el tema se puede consultar la siguiente dirección: 
[How to use GridBagLayout](http://java.sun.com/docs/books/tutorial/uiswing/layout/gridbag.html)

`GridBagLayout` es uno de los gestores de layout que proporciona Java/Swing.
En mi opinión es el gestor más flexible, pero también el más complejo, de hecho
parece pensado para ser usado por constructores de interfaces gráficas, como por
ejemplo Matisse para NetBeans.

<!-- more -->

Lo primero de todo veamos qué se puede conseguir con este gestor de layout:

![Ventana usando `GridBagLayout`]({{ site.baseurl }}/assets/images/wordpress/gridbaglayout-frame1.png)

`GridBagLayout` coloca los componentes en una serie de filas y columnas, permite 
a los componentes ocupar varias filas y/o columnas y las filas y las columnas no 
tienen porque tener la misma altura o anchura. Finalmente, `GridBagLayout` calcula 
estas alturas y anchuras dependiendo de los atributos preferredSize de los componentes. 
En la siguiente imagen podemos el diseño de cada una de las celdas en las que se 
divide `GridBagLayout`:

![Diseñando un panel con `GridBagLayout`]({{ site.baseurl }}/assets/images/wordpress/gridbaglayout-design.png)

Los componentes indican a `GridBagLayout` sus restricciones mediante un objeto del 
tipo `GridBagConstraints`. En esta primera entrada estudiaremos las restricciones 
básicas y dejaremos para la siguiente parámetros más avanzados que nos permitirán 
diseñar la posición y comportamiento de los componentes con máxima flexibilidad.

`gridx` y `gridy`: Indican la fila y la columna donde situar el componente. 
`gridx=0` y `gridy=0` indican la celda superior izquierda, mientras que, en 
nuestro ejemplo, `gridx=3` y `gridy=3` indican la celda inferior derecha.

`gridwidth` y `gridheight`: Indica el número de columnas o filas - respectivamente - 
que ocupa el componente. El valor por defecto es `1` y es posible que un componente 
ocupe varias filas y varias columnas a la vez, como por ejemplo `btn6`.

*Actualización*: si te ha gustado, quizá deberías ver la segunda parte 
[Uso de GridBagLayout (y II)]({{ site.baseurl }}{% post_url 2010-01-20-uso-de-gridbaglayout-y-ii %}).
