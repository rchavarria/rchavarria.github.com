---
title: "solveet: Torres de Hannoi"
date: 2012-12-12 09:35
author: Rubén Chavarría
comments: true
categories: 
- solveet
- learning
- programming workout
- JavaScript
- tdd
published: true
footer: false
sidebar: true
---

Simplemente para practicar y mejorar mis habilidades como programador, me gusta resolver problemas
de programación regularmente. Hace un tiempo conocí la página [Solveet](http://solveet.com), y desde
entonces intento aportar semanalmente alguna que otra solución a los problemas propuestos por otros
profesionales del desarrollo software.

![By André Karwath aka Aka, Own work, CC-BY-SA-2.5, via Wikimedia Commons](http://upload.wikimedia.org/wikipedia/commons/6/60/Tower_of_Hanoi_4.gif)

El problema que he solucionado esta semana es el de las 
[Torres de Hannoi](http://www.solveet.com/exercises/Torres-de-Hannoi/72), todo un clásico en el 
desarrollo software, y en este post intento describir detalladamente cómo he llegado a mi solución.

<!-- more -->

## Introducción

El punto de partida ha sido esta entrada en la wikipedia acerca de las 
[Torres de Hannoi](http://es.wikipedia.org/wiki/Torres_de_Han%C3%B3i) donde explica de una forma muy
básica la forma de solucionarlo. Ahora sólo hay que implementarlo.

Decidí solucionar el problema en javascript, para aprender más sobre este lenguaje, y decidí solucionar
el problema de forma iterativa, ya que me pareció más sencilla que la forma recursiva. Y ya que estoy
practicando, intenté llegar a la solución definitiva practicando TDD.

Puedes ver mi solución publicada en [solveet](http://www.solveet.com/exercises/Torres-de-Hannoi/72/solution-1051),
así como el código completo de la solución y los tests en este repositorio de 
[github](https://github.com/rchavarria/solveet-problems/tree/master/hannoi-js).

## Manos a la obra

La parte más fácil es mover el anillo más pequeño. Éste hay que moverlo siempre en los pasos impares,
y siguiendo siempre un de estas dos secuencias:

- Si el número de anillos es impar, hay que moverlo a las siguientes torres o varillas: 
destino -> auxiliar -> origen, y así indefinidamente
- Si el número de anillos es par, la secuencia será: auxiliar -> destino -> origen, ...

## Movimientos en los pasos pares

En los pasos pares hay que mover los anillos que no son el anillo más pequeño. El anillo a mover dependerá
del número de anillos de los que conste el problema.

Al utilizar TDD, he ido descubriendo poco a poco cómo escoger el anillo a mover y dónde moverlo:

- 1 anillo: no hace falta mover otros anillos ya que con un movimiento está solucionado.
- 2 anillos: solo es posible mover el anillo más grande a la torre destino, ya que el anillo más pequeño lo
habremos movido en el primer movimiento a la torre auxiliar.
- 3 anillos: desarrollando manualmente todos los movimientos, el anillo a mover es aquel que no está en la
torre destino y que tampoco es el anillo más pequeño.
- 4 anillos: desarrollando otra vez manualmente todos los movimientos, el anillo a mover es el menor anillo 
(sin ser el más pequeño) y se deberá mover a la única torre posible. Esta torre la sabremos porque es aquella
torre que no contiene ni el anillo más pequeño ni el anillo a mover.

A partir de los 4 anillos, la solución ya funciona con cualquier número de anillos.

#### Reconocimientos

- Imagen By André Karwath aka Aka (Own work) [CC-BY-SA-2.5](http://creativecommons.org/licenses/by-sa/2.5), 
via [Wikimedia Commons](http://commons.wikimedia.org/wiki/File%3ATower_of_Hanoi_4.gif)
