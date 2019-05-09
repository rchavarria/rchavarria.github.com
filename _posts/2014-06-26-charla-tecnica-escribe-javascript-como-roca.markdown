---
title: "Charla técnica: Escribiendo JavaScript sólido como una roca"
date: 2014-06-26 20:00
author: Rubén Chavarría
comments: true
categories: 
- talks
- JavaScript
published: true
footer: false
sidebar: true
---

Hace poco, he visto una charla técnica impartida por
[Damian Nicholson](https://twitter.com/damian)
titulada *Writing (testable | maintainable | scalable | rock solid) JavaScript*,
que traduzco libremente como *Escribiendo JavaScript sólido como una roca*.

En la charla, Damian analiza varios aspectos de porqué es difícil testear
cierto código JavaScript y finaliza contando su experiencia escribiendo código
para evitar todos esos errores. 

<!-- more -->

<iframe src="//player.vimeo.com/video/68526881" width="500" height="161" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

### Consejos

A lo largo de la charla, Damian suelta unos cuantos pequeños consejos:

1. JavaScript + Unit testing = Good code
2. Apóyate en los objetos. Según el conferenciante, los objetos te llevarán a 
diseñar clases, éstas a agruparlas en módulos, y los módulos a organizar mejor
tus ficheros JavaScript.
3. Sobretodo, uno debería testear su API pública, aunque no limitarse a ella.

### Problemas a la hora de testear código JavaScript

A través de un sencillo snipet de código, Damian expone algunos de los problemas
más comunes a la hora de escribir código JavaScript que lo hace difícilmente
testeable:

- Funciones anónimas.
- Acoplamiento fuerte con el DOM, por ejemplo en el uso y abuso de ids en elementos
HTML
- Hacer llamadas al servidor mezcladas con otra lógica de nuestra aplicación.
- Callbacks anidados.
- Mezclar código HTML y JavaScript, por ejemplo, excribiendo *templates* HTML a 
fuego en JavaScript.

### Su propia experiencia

- usar data-attributes para parametrizar, o configuraciones. Depender menos de ids
en los elementos HTML.
- Conocer el ciclo de vida de los frameworks que utilizamos, y *engancharnos* a los
eventos del ciclo que dirigen el proceso.
- Aislar nuestra aplicación de los detalles de plugins de terceros (gran consejo éste).
- Apóyate en [mixins](http://lostechies.com/derickbailey/2012/10/07/javascript-mixins-beyond-simple-object-extension).
Con ellos podrás extender la funcionalidad de tus objetos, de una forma parecida a
la herencia, aunque muy diferente a ella.
- Mantén funcionalidades privadas en ámbitos privados
(patrón [módulo](http://www.codeproject.com/Articles/247241/Javascript-Module-Pattern)).

### Conclusión

Es una charla eminentemente práctica, por lo que es totalmente recomendable
si quieres conocer de primera mano buenos consejos sobre cómo escribir código
JavaScript testeable.

No estoy de acuerdo en todos los consejos que comenta Damian, pero la voz de
la experiencia tiene muchísimo valor, por lo que la charla me parece fenomenal.
