---
title: "Charla técnica: Is TDD dead? Of course not!"
date: 2015-01-17 17:35
author: Rubén Chavarría
comments: true
categories: 
- talks
- tdd
published: true
footer: false
sidebar: true
---

Hace poco, vi posteada una charla de [Emily Bache] titulada [Is TDD dead? Of course not!]
en el blog [Garajeando], un blog que suelo leer. Poco después la vi posteada
en otro blog que suelo leer, [The long way through Software Craftsmanship]. ¿Algo debería tener
la charla no? Aquí hay un resumen de lo que la charla me a aportado a mí:

<!-- more -->

Básicamente, la charla habla de las tres críticas que [David Heinemeier Hansson]
hizo a la práctica de TDD con su [TDD is dead, long live testing].

1. Fundamentalismo: para evitarlo, experimenta TDD, inténtalo por tí mismo, que no
te lo cuenten. Después, juzga por tí mismo. Para experimentarlo existen prácticas
como las *code katas* o *coding dojos* y herramientas como [cyber-dojo.org].
2. Daña el diseño: diseñar es difícil (con o sin TDD). TDD
te empuja a introducir nuevos niveles de indirección, hacia el Principio de
Inversión de Dependencias. Aún así, es **tu responsabilidad** como programador
saber cuándo tu aplicación tiene demasiados niveles de indirección y actuar en
consecuencia.
3. Foco en tests unitarios: puede que David tenga razón aquí, hay mucho foco
en los tests unitarios. Emily nos habla de unos [tests de Aprobación] como 
complemento a los unitarios.

Un montón de consejos (la mayoría) sobre TDD son para principiantes de TDD.
Así que, cuando te den alguno, piensa si ya has superado esa barrera, y si lo
has hecho, ignora el consejo, porque tú ya estas por encima de él. Aprende a
discernir qué información es válida para tu nivel.

<iframe width="560" height="315" src="//www.youtube.com/embed/PCEHRFHKZSk" frameborder="0" allowfullscreen></iframe>

[Emily Bache]: http://twitter.com/emilybache
[Is TDD dead? Of course not!]: https://www.youtube.com/watch?v=PCEHRFHKZSk
[Garajeando]: http://garajeando.blogspot.com/2015/01/interesting-talk-is-tdd-dead-of-course.html
[The long way through Software Craftsmanship]: http://alvarogarcia7.github.io/blog/2015/01/06/talk-is-tdd-dead-of-course-not-by-emily-bache
[David Heinemeier Hansson]: http://twitter.com/dhh
[TDD is dead, long live testing]: http://david.heinemeierhansson.com/2014/tdd-is-dead-long-live-testing.html
[cyber-dojo.org]: http://cyber-dojo.org
[tests de Aprobación]: http://coding-is-like-cooking.info/tag/approval-testing
