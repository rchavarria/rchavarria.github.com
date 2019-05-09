---
title: "Programación reactiva en JavaScript"
date: 2017-12-12 22:13
author: Ruben Chavarria
comments: true
categories: 
- 
published: true
footer: false
sidebar: true
---

¿Qué falta en JavaScript para completar el siguiente cuadrante? Para elementos
únicos y de forma síncrona, tenemos las variables y las llamadas a los métodos.
Para múltiples elementos de forma síncrona, tenemos los arrays. Para elementos
únicos, pero asíncronos, las promesas (`Promise`).

![ReactiveX]({{ site.baseurl }}/assets/images/2017/cuadrante-reactivex.png)

<!-- more -->

Existe una herramienta o paradigma (la verdad es que no sé muy bien cómo
llamarlo) que está cobrando fuerza y popularidad últimamente, sobre todo por su
uso en frameworks muy conocidos como React o Angular. Se trata de la
**programación reactiva**. Más concretamente, en el mundo JavaScript,
encontramos [RxJS], una implementación de [ReactiveX].

ReactiveX es una librería para componer aplicaciones asíncronas y basadas en
eventos usando secuencias observables. Es un API para trabajar con flujos
observables de datos de forma asíncrona. Combina ideas del [patrón Observer],
también conocido como pub/sub o event listener, del patrón Iterable y de la
programación funcional (funciones puras, combinación de funciones,...).

ReactiveX es muy versátil, proporciona funcionalidades para el backend
(asíncronía, concurrencia) y para el frontend (eventos de la interfaz gráfica,
llamadas HTTP). Es en la parte cliente donde la implementación RxJS cobra
fuerza. Se podría utilizar en el backend, sobre Node.js, pero parece más
natural usar JavaScript en el navegador.

La programación reactiva se basa en 3 pasos: **crear** (crea flujos de eventos o
flujos de datos), **combinar** (compone y transforma flujos mediante operadores) y
escuchar/reaccionar/**observar** mediante suscripciones a los `Observable`s. De
ella podríamos destacar las siguientes cualidades:

1. Favorece la composición
2. Es flexible, permite trabajar con 1 elemento, varios o infinitos
3. Es funcional, nos permite aplicar funciones puras a los flujos de datos
4. Facilita la concurrencia, `Observable`s y `Scheduler`s nos permiten dejar
a un lado temas de concurrencia, sincronización e hilos

Como ha quedado un artículo muy teórico, veamos cómo podemos crear y consumir
nuestro primer `Observable`. En los siguientes artículos explicaremos cada una
de las partes y veremos qué opciones nos ofrece RxJS.

```javascript
Observable.from([ 1, 2, 3 ])
  .subscribe(i => {
    console.log('index:', i)
  })

/* output
index: 1
index: 2
index: 3
*/
```

Este código y más, está disponible en el repositorio de GitHub
[reactive-programming-rxjs].

En el próximo artículo veremos en detalle cómo crear un flujo observable a
partir de un array y de cómo se compararía con un array síncrono.

[RxJS]: http://reactivex.io/rxjs/
[ReactiveX]: http://reactivex.io/
[patrón Observer]: http://en.wikipedia.org/wiki/Observer_pattern
[reactive-programming-rxjs]: https://github.com/rchavarria/reactive-programming-rxjs
