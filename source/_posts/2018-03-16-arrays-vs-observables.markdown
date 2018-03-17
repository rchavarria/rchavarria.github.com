---
layout: post
title: "Programación reactiva con RxJS: comparando arrays con Observables"
date: 2018-03-16 14:00
author: Ruben Chavarria
comments: true
categories: 
- reactivex
- javascript
published: true
footer: false
sidebar: true
---

En el cuadrante del [artículo anterior] vimos cómo los *Observables* podrían
verse como arrays asíncronos.

Los arrays son síncronos, y por lo tanto, se iteran síncronamente. En cambio,
los Observables son *observados* (bienvenido Capitán Obvio) y *reaccionan* en
cuanto hay un nuevo valor presente en el flujo asíncrono.

{% img center /images/2018/bees.jpg %}

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/JXSQNN">Bees</a> de <a href="https://www.flickr.com/photos/kbphoto/">Keith</a>, <a href="https://creativecommons.org/licenses/by-nc-nd/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by-nc-nd/2.0/">CC BY-NC-ND 2.0</a>
  </span>
</div>

<!-- more -->

A mancharnos las manos con código, que es a lo que hemos venido. Comparemos
cómo iterar un array y un flujo (por ahora síncrono, no abandones todavía) de
elementos observables.

```
// array
[ 1, 2, 3 ].forEach(i => console.log(i));
// salida:
// 1
// 2
// 3

// observable
Observable.from([ 1, 2, 3 ])
    .subscribe(i => console.log(i));
// salida:
// 1
// 2
// 3
```

<div style="text-align: center">
  <span style="font-size: 60%">
    Hay una versión ejecutable de este código en GitHub, en el fichero <a href="https://github.com/rchavarria/reactive-programming-rxjs/blob/master/02-arrays-vs-observables/01-array-vs-observable.js">01-array-vs-observable.js</a>
  </span>
</div>

En este primer ejemplo la diferencia no es muy grande. Incluso la función
pasada a `forEach` y a `subscribe` podría ser la misma. Más adelante veremos
mayores diferencias.

Como vemos, con `Observable.from` podemos crear un `Observable` a partir de un
array. Pero también podemos crearlos a partir de otras fuentes, por ejemplo, a
partir de eventos generados por el usuario o generados programáticamente, pero
para este ejemplo, `.from` nos puede servir.

Para procesar los elementos del flujo, debemos pasar una función a `subscribe`.
En realidad, `subscribe` admite los siguientes usos:

1-. El más sencillo, el paso de una función, conocida como `next`, que será
llamada una vez por cada elemento del flujo. La función `next` admite recibe
dicho elemento como primer parámetro

2-. Pasar tres funciones: `next`, `error` y `completed`. Ya conocemos el uso de
`next`, `error` es autoexplicativo, y `completed` es llamada cuando ya no hay
más elementos en el flujo.

```
Observable.from([ 1, 2, 3, ])
    .subscribe(
        (item) => console.log('`next` processes:', item),
        (e) => console.error('`error` receives:', e),
        () => console.log('Completed!')
    );

// salida:
// `next` processes: 1
// `next` processes: 2
// `next` processes: 3
// Completed!
```

<div style="text-align: center">
  <span style="font-size: 60%">
    Hay una versión ejecutable de este código en GitHub, en el fichero <a href="https://github.com/rchavarria/reactive-programming-rxjs/blob/master/02-arrays-vs-observables/02-next-error-complete.js">02-next-error-complete.js</a>
  </span>
</div>

3-. En lugar de pasar las tres funciones, podemos pasar un objeto que
implemente al menos tres funciones con los nombres anteriormente vistos. En
este caso, estaríamos *implementando* el interfaz `Observer` (en caso de que se
pudieran escribir o implementar interfaces en JavaScript).

```
const myObserver = {
    next: (item) => console.log('`next` processes:', item),
    error: (e) => console.error('`error` receives:', e),
    complete: () => console.log('Completed!')
};

Observable.from([ 1, 2, 3, ])
    .subscribe(myObserver);

// salida:
// `next` processes: 1
// `next` processes: 2
// `next` processes: 3
// Completed!
```

<div style="text-align: center">
  <span style="font-size: 60%">
    Hay una versión ejecutable de este código en GitHub, en el fichero <a href="https://github.com/rchavarria/reactive-programming-rxjs/blob/master/02-arrays-vs-observables/03-first-observer.js">03-first-observer.js</a>
  </span>
</div>

En este artículo hemos visto lo parecido que es consumir un `Observable` a
consumir un `array`, al menos en el uso más básico. Pero hemos empezado a ver
alguna diferencia.

En la siguiente entrega veremos cómo podemos tomar un mayor control sobre
cuándo se llama a `error` y `completed`. También veremos la equivalencia de
esos métodos en la iteración de los arrays.

## Referencias

- [ReactiveX]
- [Observable] object
- [Observer] interface

[artículo anterior]: /blog/2017/12/12/programacion-reactiva-javascript/
[ReactiveX]: http://reactivex.io/
[Observable]: http://reactivex.io/rxjs/class/es6/Observable.js~Observable.html
[Observer]: http://reactivex.io/rxjs/class/es6/MiscJSDoc.js~ObserverDoc.html

