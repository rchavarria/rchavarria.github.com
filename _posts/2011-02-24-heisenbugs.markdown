---
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

> ¡Bien! Ya tengo mi nueva funcionalidad implementada. La aplicación va a ser de lo 
mejorcito con lo que acabo de desarrollar. Llevo depurando este código toda la tarde. 
¿Qué puede fallar? He recorrido instrucción por instrucción y todo se ejecuta según lo 
previsto.

> Lanzo la aplicación ...

> ¡WTF! ¡Un null pointer! ¡No puede ser! si lo he depurado miles de veces.

¿Nunca os habéis encontrado con un error de este tipo?

<!-- more -->

Yo muchas veces, pero no se me había ocurrido ponerle nombre. Hace poco, mientras leía 
[Java concurrency in practice](http://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601)
de Brian Goetz (y otros autores) encontré el nombre, y me gustó tanto que decidí escribir 
sobre ello. Mucho tiempo después aquí está la entrada.

El nombre en cuestión es **heisenbug**. Me gustó mucho porque mezcla con sentido del humor 
los conceptos de *bug* (estoy hablando de un error en una aplicación, ¿recuerdas?) y 
*Heisenberg*. La mezcla de este segundo concepto es lo que me hizo gracia: se refiere a un 
bug que aparentemente no somos capaces de reproducirlo, por lo que no podemos conocer dónde 
se está produciendo, es decir, su *posición*. Es similar al 
[principio de incertidumbre](http://es.wikipedia.org/wiki/Relaci%C3%B3n_de_indeterminaci%C3%B3n_de_Heisenberg)
de [Werner Heisenberg](http://es.wikipedia.org/wiki/Werner_Heisenberg), que en palabras 
llanas dice:

> No se puede determinar, en términos de la física clásica, simultáneamente y con precisión 
arbitraria, ciertos pares de variables físicas, como son, por ejemplo, la posición y el 
momento lineal de una partícula (digamos un electrón)

En realidad, el problema siempre ha estado ahí, pero no se dieron las condiciones adecuadas 
para que el error *apareciera*, es decir, no hemos sido capaces de conocer su 
*posición*.

No viene a cuento, pero [Microsiervos](http://www.microsiervos.com) lleva una temporada 
publicando términos que podrían incluirse en un 
[geekcionario](http://www.microsiervos.com/archivo/microciervadas-varias/geekccionario-04.html),
entre los cuales podría encajar *heisenbug*.

Nota: Los autores de *Java concurrency in practice* son: Brian Goetz, Tim Peierls, 
Joshua Bloch, Joseph Bowbeer, David Holmes y Doug Lea.
