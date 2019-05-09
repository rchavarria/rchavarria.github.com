---
title: "Learning JavaScript design patterns"
date: 2015-05-29 01:04
author: Rubén Chavarría
comments: true
categories: 
- Reseñas
- JavaScript
published: true
footer: false
sidebar: true
---

##### de Addy Osmany

## Por qué lo he leído

![JavaScript desing patterns](http://www.addyosmani.com/resources/essentialjsdesignpatterns/cover/cover.jpg)

Ya llevo un tiempo programando con JavaScript de forma profesional, y empiezo
a sentir que necesito ir un paso más allá con el lenguaje. No creo que conozca
todo lo que ofrece el lenguaje, todo lo contrario, a veces siento que me queda
mucho por aprender y que necesito profundizar en muchos y muchos temas. Con
este libro pretendía trasladar mis conocimientos sobre patrones de diseño con
Java a JavaScript.

<!-- more -->

## Qué esperaba

Esperaba grandes cosas de este libro. Ya tenía referencias anteriores del autor,
creo que es un profesional como la copa de un pino. Así que un libro escrito
por él, pues tenía buena pinta.

Supongo que esperar encontrar una estructura de libro muy parecido a otros:
clasificaciones, descripciones, catalogaciones,...

## Qué encontré

Encontré un libro con mucho código, cosa que no tiene que ser ni bueno, ni malo.
En el caso de este libro, es una ayuda muy buena. Las explicaciones de Addy son
clarísimas y hay multitud de ejemplos y casos reales.

## Conclusiones

Aunque es un libro que no miente, trata sobre patrones de diseño, el libro me
ha defraudado un poco. Esperaba más del autor. Quizá no he sabido aprovechar
el contenido del libro, pero me ha parecido superficial en algunos capítulos,
y en otros ha entrado a describir con mucho detalle librerías como jQuery o
plugins para él.

En realidad, el libro que andaba buscando era [JavaScript patterns], de
Stoyan Stefanov, pero me daba más confianza Addy porque era un autor que ya
conocía. Toca ponerle remedio y ya me he puesto con el libro de Stoyan.

Eso sí, tengo que reconocer que es el primer lugar donde he encontrado una buena
descripción de lo que son cada una de las arquitecturas MVx (MVC, MVP, MVVM,...)

## Qué he aprendido

- Se pueden añadir propiedades a objetos a través del método
`Object.defineProperties()`
- Los métodos de un objeto, no se deben declarar en la función constructor, sino
modificando el prototipo de la misma
- Se debe intentar conseguir un bajo acoplamiento, algunos patrones (Observer,
Mediator,...) ayudan a ello
- Mixins
- Patrón Flyweight, consiste en agrupar o manejar conjuntamente funcionalidades
que pueden compartir un subconjunto de sus datos
- Diferencias entre los distintos MVx

    - En MVC, las Vistas tienen acceso directo al Modelo
    - En MVP, los Presentadores escuchan eventos de la Vista y del Modelo y median en la acciones entre ellos
    - MVVM nos permite crear partes específicas de las Vistas de un Modelo en concreto

- Expresiones de Función Inmediatamente Invocadas (IIFE - Immediately-Invoked Function Expressions)

## Recursos relacionados

- [Learning JavaScript design patterns], by Addy Osmani
- [Sintaxis definitiva de módulos]
- [Notas tomadas]
- [JavaScript patterns], de Stoyan Stefanov

[Learning JavaScript design patterns]: http://www.addyosmani.com/resources/essentialjsdesignpatterns/book
[Sintaxis definitiva de módulos]: http://www.2ality.com/2014/09/es6-modules-final.html
[Notas tomadas]: https://github.com/rchavarria/blog-post-incubator/blob/master/published-book-notes/learning-javascript-design-patterns-by-addy-oshmany.markdown
[JavaScript patterns]: https://amzn.to/2Ose83Z
