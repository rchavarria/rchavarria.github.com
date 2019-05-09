---
layout: post
title: "Curso sobre RxJS"
date: 2018-11-13 00:00
author: Ruben Chavarria
categories:
- Cursos
- JavaScript
- Programación Reactiva
---

Notas tomadas durante la realización del curso de Pluralsight
[RxJS: Getting started] de [Brice Wilson].

Es un curso (parece que bastante completo) sobre programación reactiva en JavaScript.
Tiene conceptos que ya he aprendido en otro momento, pero al trabajar con Angular
siento que necesito profundizar en algunos conceptos de [RxJS]. Veamos si este
curso me sirve para ampliar mis conocimientos en este tema.

<!-- more -->

Índice:

- Course Overview
    - Course Overview

- Reactive Programming Basics
    - What Is RxJS?
    - Imagining Data as a Stream
    - RxJS Building Blocks
    - Demo Project Overview
    - Compatibility Packages for RxJS 5

- Creating Observables
    - Observables and Observers
    - Instantiating a New Observable with the Constructor
    - Creating Observables from Existing Data
    - Creating Observables to Handle Events
    - Making AJAX Requests with RxJS
    - Summary

- Subscribing to Observables with Observers
    - Introduction
    - Understanding Observers
    - Creating and Using Observers
    - Executing Observables
    - Multiple Observers Executing a Single Observable
    - Managing Subscriptions
    - Cancelling Observable Execution with a Subscription
    - Summary

- Using Operators
    - Introduction
    - Applying Operators
    - Categories of Operators
    - Reading a Marble Diagram
    - Importing and Using Common Operators
    - Handling Errors
    - Controlling the Number of Values Produced
    - Summary

- Creating Your Own Operators
    - Why Create Your Own Operators?
    - Structure of an Operator
    - Creating New Operators with the Observable Constructor
    - Creating New Operators from Existing Operators
    - Summary

- Using Subjects and Multicasted Observables
    - Introduction
    - What Are Subjects?
    - Producing Values with Subjects
    - Cold vs. Hot Observables
    - Using a Subject to Convert an Observable from Cold to Hot
    - Multicasting Operators
    - Using Multicast Operators Instead of Subjects
    - Specialized Subjects
    - Controlling Multicasted Output with Specialized Operators
    - Summary

- Controlling Execution with Schedulers
    - What Are Schedulers?
    - RxJS Schedulers
    - Understanding Schedulers and the Event Loop
    - Using Schedulers with Observable Creation Functions
    - Applying a Scheduler with the observeOn Operator
    - Summary

- Testing Your RxJS Code
    - Introduction
    - Using the TestScheduler
    - Observable and Subscription Marble Syntax
    - Structuring Unit Tests
    - Testing Observables and Subscriptions with Marble Diagrams
    - Summary

## Notas tomadas

### Capítulo 3: Creating Observables

Formas básicas de crear observables:

```javascript
const source1$ = of(1, 'hello', 1.11)
const source2$ = from([ 1, 'hello', 2.22 ])
const button = document.getElementById('some-button')
const source3$ = fromEvent(button, 'click')

// AJAX calls
import { ajax } from 'rxjs/ajax'
ajax('/server/path')
  .subscribe(ajaxResponse => {
    console.log(ajaxResponse.status)  // 200 (http ok)
    console.log(ajaxResponse.response)
  })
```

### Capítulo 4: Subscribing to Observables with Observers

Cuando se *ejecuta* un observable?

1. Cuando se llama al método `subscribe`
2. Cada vez que un observer se suscribe llamando a `subscribe` se realiza
una *ejecución* independiente del observable

El método `subscribe` devuelve un objecto llamado *suscripción*, que permite
cancelar la suscripción, entre otras cosas.

```javascript
const timer$ = interval(1000)
const subscription = timer$.subscribe(/* ... */)
setTimeout(() => subscription.unsubscribe(), 5000) // will cancel after 5s
```

### Capítulo 5: Using Operators

El cambio de API que hubo de la versión 5 a la 6 de RxJS vino para hacer más fácil
para las herramientas de bundling (como Webpack) utilizar *tree shaking* para
optimizar código. Así, RxJS pasó de esto a esto:

```javascript
of(1, 2, 3)
  .map(/* ... */)
  .filter(/* ... */)

of (1, 2, 3).pipe(
  map(/* ... */),
  filter(/* ... */)
)
```

Algo muy útil es aprender a leer los diagramas que describen los operadores, los
*marble diagrams* o *Diagramas de canicas*

Otro aspecto muy importante es cómo gestionar los errores. Se pueden capturar errores
con el operador `catchError`. Y tenemos varias opciones:

1. Devolver otro observable, de forma que el observer no sabrá que ha habido un error

```javascript
ajax('/some/api').pipe(
  map(/* ... */),
  filter(/* ... */),
  catchError(err => of(new ANewResponseFromMine())
)
.subscribe(
  val => console.log('observed val:', val),
  err => console.log('ERRRRR', err)
)

// we'll see:
// observe val: ...
```

2. Hacer algo con el observable que causó el error:

```javascript
ajax('/some/api').pipe(
  map(/* ... */),
  filter(/* ... */),
  catchError(err, caught => {
    // do sthg with the observable `caught`
  })
)

3. Lanzar otro error completamente distinto:

```javascript
ajax('/some/api').pipe(
  map(/* ... */),
  filter(/* ... */),
  catchError(err => throw 'a complete new error')
)
.subscribe(
  val => console.log('observed val:', val),
  err => console.log('ERRRRR', err)
)

// we'll see:
// ERRRRRR ....
```

4. O lanzar un error pero como observable:

```javascript
import { throwError } from 'rxjs/operators'
// ...
catchError(err => return throwError('a complete new error'))
// ...
```

### Capítulo 6: Creating Your Own Operators

Un operador no es más que una función que devuelve una función. La función
devuelta admite un observable como parámetro y debe devolver otro observable.
Puedes usar operadores existentes para implementar el tuyo propio.

```javascript
function myOperator(myArg1, myArg2, ...) {
  return function (source$) {
    return myNewObservable$
  }
}
```

Creando un operador a partir de operadores ya existentes:

```javascript
function grabClassics(year) {
  // el operador `filter` devuelve una función cuyo argumento es un obsvble y 
  // esa misma función devuelve otro obsvble
  return filter(book => book.publicationYear < year)
}
```

### Capítulo 7: Using Subjects and Multicasted Observables

**Subject**: son Observables (pueden ser observados), pero también son Observers
(por lo que pueden observar a otros Observables). Mantienen una lista de Observers,
luego son multicast en lugar de unicast. Eso quiere decir que el mismo valor puede
ser enviado a varios Observers sin tener que *ejecutar* un Observable varias veces.

**Cold observable**: 

- El productor de valores se crea dentro mismo del observable
- On observer por *ejecución*
- Unicast
- Ejemplos: `interval`, `ajax`,...

**Hot observable**:

- El productor de valores existe fuera del observable (produce valores haya o no
observers)
- Un productor compartido permite varios observers
- Multicast
- Ejemplos: `fromEvent`,...

Subjects permiten convertir un *cold* en un *hot* observable.

```javascript
const source$ = interval(1000).pipe(/* ... */)
const subject$ = new Subject()

// Subjects are observers
source$.subscribe(subject$)

// Subjects are observables too
subject$.subscribe(v => console.log('#1', v))
subject$.subscribe(v => console.log('#2', v))
subject$.subscribe(v => console.log('#3', v))

// Observable `interval` got just one subscription, the one from the subject
```

Pero ya existen operadores multicast: `multicast`, `refCount`, `publish`, `share`,...

Hermandos de estos operadores, existen otros operadores que usan Subjects especializados
en alguna tarea: reconnectarse, emitir el último valor, emitir el primero,... (`publishLast`,
`publishReplay`,...)

### Capítulo 8: Controlling Execution with Schedulers

**Schedulers**: controlan cuándo un observable es ejecutado: `queueScheduler`,
`asapScheduler`, `asyncScheduler`, `TestScheduler`,...

Cada uno de ellos se encola en una pila de tareas de JavaScript:

- `queue`: en la principal
- `asap`: en la asíncrona de micro tareas
- `asyn`: en la asíncrona

*Mirar cómo funciona el bucle de eventos de JavaScript (loop event) para entender
cómo funcionan esas pilas*

Normalmente se puede pasar un scheduler a los operadores que crean observables

```javascript
import { queueScheduler, of } from 'rxjs'
const source$ = of(1, 2, 3, 4, queueScheduler)
// ...
```

Con el operador `observeOn` podemos cambiar el Scheduler de un observable. Útil por
ejemplo para no bloquear el UI con un observable que va a tardar mucho, planificándolo
con el `asyncScheduler`.

### Capítulo 9: Testing Your RxJS Code

`TestScheduler` te permite probar código asíncrono de forma síncrona.

Primero hay que crear una instancia del scheduler, pasándole como parámetro una función
donde comprobaremos los valores. Para ejecutar el código, debemos llamar al método
`run` del scheduler, pasándole una función como parámetro. Esta función tiene
un parámetro, `helpers`, el cual tiene unos cuantos métodos muy útiles para probar
nuestros observables: `cold`, `hot`, `expectObservable`, `expectSubscriptions`, `flush`.

```javascript
const scheduler = new TestScheduler((actual, expected) => {
  // perform deep equality test
})

scheduler.run(helpers => {
  // helpers.cold()
  // helpers.hot()
  //...
})
```

Los métodos `cold` y `hot` utilizan una sintaxis especial (marble syntax) para definir
cómo funciona el observable.

```javascript
const source$ = helpers.cold('-a-b-c') // each character is a *virtual ms*
const source$ = helpers.cold('--a-4---c-8|')  // | ends the stream
const source$ = helpers.cold('  --a-4 12ms c-8#') // 12ms replaces 12 dashes
const source$ = helpers.hot('-a-^-b-(cde)---f|') // ^ marks when the subscription is done, only for hot
                                                 // (cde) emits 3 values at the same time
                                                 
// subscriptions
const subscription = '^---!'
const subscription = '---^-' // never ends
const subscription = '^ 10ms !'
```

Un test de ejemplo sería más o menos así:

```javascript
it('...', () => {
  const scheduler = new TestScheduler((actual, expected) => {
    // mocha/chai
    expect(actual).deep.equal(expected)
  })
  
  scheduler.run(helpers => {
    const source$ = helpers.cold('-a-b-c-d|')
    const expected =         '5ms -a-b-c-d|'
    
    helpers.expectObservable(source$.pipe(
      delay(5)
    ))
    .toBe(expected)
  })
})
```

[RxJS: Getting started]: https://app.pluralsight.com/library/courses/rxjs-getting-started/table-of-contents
[Brice Wilson]: http://www.bricewilson.net/
[RxJS]: https://www.learnrxjs.io/
