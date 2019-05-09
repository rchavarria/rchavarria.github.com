---
layout: post
title: "Seven Ineffective Coding Habits of Many Programmers"
date: 2018-07-03 00:00
author: Ruben Chavarria
categories:
- Charlas
- Buenas prácticas
---

Charla de [Kevlin Henney] sobre [7 hábitos poco efectivos de muchos programadores]
donde habla precisamente de eso, de ciertos hábitos perjudiciales para
trabajar en equipo.

<!-- more -->

Los hábitos de los que habla no son gran cosa, no ha descubierto nada realmente
espectacular, pero sí me quiero quedar con una cita/frase que aparece en
una slide (redactada al estilo de una historia de usuario):

> Como programador, quiero programar para comunicar de forma directa e intencionada,
de forma que pueda pasar menos tiempo determinando el significado del código
fuente y más tiempo programando significativamente

Repito, en inglés para que no se pierda nada:

> ... I can spend less time determining the meaning of code and more time
coding meaningfully

Los 7 hábitos poco efectivos de los que habla:

1. Código ruidoso: malos comentarios, mal estilo de programación, dependencias
no necesarias,...
2. Espaciamiento: mala alineación del código, mala alineación de parámetros,
líneas excesivamente largas,...
3. Nombrado: nombres redundantes o excesivamente largos
4. Abstracción insuficiente: abuso de tipos primitivos, no hablar el lenguaje de
Negocio
5. Estado no encapsulado: getters y setters por todos los lados, o setters donde
solo se debería usar getter
6. Tests no coherentes: básicamente, tests que prueban varias cosas a la vez, o que
tienen más de un punto de fallo y no identifican claramente la causa del fallo

*Me falta uno, no se qué ha pasado con él*

[Kevlin Henney]: http://kevlin.eu
[7 hábitos poco efectivos de muchos programadores]: https://www.youtube.com/watch?v=SUIUZ09mnwM
