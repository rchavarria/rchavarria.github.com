
---
layout: page
title: "Heisenbugs"
date: 2011-02-24 02:24
author: Rubén Chavarría
categories: 
- software
- internet
- java
comments: true
published: true
footer: false
sidebar: true
---

<blockquote>¡Bien! Ya tengo mi nueva funcionalidad implementada. La aplicación va a ser de lo mejorcito con lo que acabo de desarrollar. Llevo depurando este código toda la tarde. ¿Qué puede fallar? He recorrido instrucción por instrucción y todo se ejecuta según lo previsto.

Lanzo la aplicación ...

¡WTF! ¡Un null pointer! ¡No puede ser! si lo he depurado miles de veces.</blockquote>

¿Nunca os habéis encontrado con un error de este tipo?

<!-- more -->

Yo muchas veces, pero no se me había ocurrido ponerle nombre. Hace poco, mientras leía <a href="http://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601">Java concurrency in practice</a> de Brian Goetz (y otros autores) encontré el nombre, y me gustó tanto que decidí escribir sobre ello. Mucho tiempo después aquí está la entrada.

El nombre en cuestión es <strong>heisenbug. </strong>Me gustó mucho porque mezcla con sentido del humor los conceptos de <em>bug</em> (estoy hablando de un error en una aplicación, ¿recuerdas?) y <em> Heisenberg</em>. La mezcla de este segundo concepto es lo que me hizo gracia: se refiere a un bug que aparentemente no somos capaces de reproducirlo, por lo que no podemos conocer dónde se está produciendo, es decir, su <em>posición. </em>Es similar al <a title="principio de incertidumbre" href="http://es.wikipedia.org/wiki/Relaci%C3%B3n_de_indeterminaci%C3%B3n_de_Heisenberg">principio de incertidumbre</a> de <a title="Werner Heisenberg" href="http://es.wikipedia.org/wiki/Werner_Heisenberg">Werner Heisenberg</a>, que en palabras llanas dice:
<blockquote>No se puede determinar, en términos de la física clásica, simultáneamente y con precisión arbitraria, ciertos pares de variables físicas, como son, por ejemplo, la posición y el momento lineal de una partícula (digamos un electrón).</blockquote>
En realidad, el problema siempre ha estado ahí, pero no se dieron las condiciones adecuadas para que el error <em>apareciera</em>, es decir, no hemos sido capaces de conocer su <em>posición</em>.

No viene a cuento, pero <a href="http://www.microsiervos.com">Microsiervos </a>lleva una temporada publicando términos que podrían incluirse en un <em><a href="http://www.microsiervos.com/archivo/microciervadas-varias/geekccionario-04.html">geekcionario</a></em>, entre los cuales podría encajar <em>heisenbug.</em>

Nota: Los autores de <em>Java concurrency in practice</em> son: Brian Goetz, Tim Peierls, Joshua Bloch, Joseph Bowbeer, David Holmes, Doug Lea.