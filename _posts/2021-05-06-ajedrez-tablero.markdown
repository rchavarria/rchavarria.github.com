---
layout: post
title: "Ajedrez: leer el tablero"
date: 2021-05-06 06:05
author: Ruben Chavarria
categories: 
- Aprender
- Ajedrez
- Learning
---

Esta pequeña nota forma parte de mi camino sobre profundizar en mi
[aprendizaje del ajedrez][1], en el apartado sobre las lecciones que puedes
encontrar y seguir en la [plataforma chess.com][2].

Y hoy toca hablar acerca de leer el tablero:

<!-- more -->

### Estructuras de peones

Los peones conectados pueden defenderse y ayudarse entre ellos según van avanzando.
Los doblados, en cambio, se bloquean entre sí, e impiden avanzar. Los que no
tienen a ningún peón cerca son peones aislados, y suelen ser más fáciles de
atacar

Se suele decir que los peones son el alma del ajedrez

Los peones son más fuertes cuando juegan juntos, pero débiles cuando lo hacen
de forma separada

Un grupo de peones conectados se les suele llamar *isla de peones*. Cuantas más
islas tengas, peor, significa que hay desconexión entre tus peones

### Cadenas de peones

Un grupo de peones que se protegen unos a otros formando una diagonal, se llama
una *cadena de peones*. El único peón desprotegido es el peón base, al principio
de la cadena. Esta formación es una de las más fuertes

Una cadena de peones puede restringir los movimientos del adversario y ayudarse
entre ellos a avanzar al final del juego

Incluso una pequeña cadena de dos peones pueden hacer frente a una poderosa
torre (normalmente al final del juego)

Pero no siempre la mejor forma de atacar una cadena es atacando la base, a veces,
es preferible atacar al peón más avanzado, intercambiar algunos peones y hacer
la cadena de nuestro oponente más corta (y débil)

### Espacio

Cuanto más espacio controlas en el tablero, más libres son tus piezas para
maniobrar, y menos lo son las de tu adversario

Una buena forma de reclamar espacio para tí es controlar el centro con los
peones

### Juegos abiertos, cerrados y semi-abiertos

Hay posiciones donde hay pocos peones en el juego. Son posiciones *abiertas*. En
este tipo de posiciones, los alfiles tienen más libertad de movimientos y por
lo tanto son más poderosos.

Hay otras posiciones, donde hay muchos peones en el juego. Se llaman posiciones
*cerradas*. En ellas, los alfiles tienen los movimientos más restringidos, y son
los caballos los que suelen encontrar casillas donde moverse, por lo tanto, aquí
son más poderosos los caballos que los alfiles

En otras ocasiones, ni para tí ni para mi. Son las posiciones *semi-abiertas*.
Y dependerá de otros factores para considerar los alfiles más poderosos que los
caballos o al contrario

En estas últimas, hay que ser lo más flexible posible. Estando atento a la 
apertura de columnas y diagonales, por si acaso la posición se abre. O encontrando
buenas casillas para nuestras piezas, si la posición se va cerrando

### Avanzar, capturar o ignorar

Veamos un poco cómo soportar la presión cuando hay peones enfrentados. ¿Deberíamos
capturar, avanzar o simplemente jugar en otro lugar del tablero?

Si puedes atacar y defender al mismo tiempo, quizá sea esa la mejor opción

Como regla general, sólo responde a las amenazas del contrario si tú no tienes
ninguna amenaza mayor con la que responder

### Cuándo intercambiar piezas

Normalmente, está bien intercambiar piezas si está claro que sales ganando en 
el intercambio. Pero... ¿qué hacer cuando ni ganas ni pierdes?

Normalmente, es un error comenzar un intercambio si no eres capaz de explicar
en qué te beneficia

Hay algunas buenas razones para saber si un intercambio es bueno:

- Simplificar, cuando tenemos una pequeña ventaja de material
- Eliminar un pieza del contrario que está bien posicionada
- Tomar el control de una columna abierta

> To take is a mistake, unless...

Comer, es un error, a no ser que tu posición mejore o la de tu oponente empeore

### Notación (de movimientos) avanzada

- Jaque = `+`
- Jaque mate = `#`
- Captura = `x`
- Coronar = `=`, (b8=Q)
- Enroque corto = `0-0`
- Enroque largo = `0-0-0`
- Buen movimiento = `!`
- Movimiento malo = `?`
- Movimiento interesante = `!?`
- Dudoso movimiento = `?!`
- Erro grave = `??`
- Grandísimo movimiento = `!!`
- Ganan blancas = `1-0`
- Ganan negras = `0-1`
- Tablas = `1/2-1/2`

[1]: {{ site.baseurl }}{% post_url 2021-02-18-aprendiendo-ajedrez %}
[2]: https://www.chess.com
