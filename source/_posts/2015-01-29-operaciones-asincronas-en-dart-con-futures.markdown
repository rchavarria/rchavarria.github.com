---
layout: post
title: "Operaciones asíncronas en Dart con Futures"
date: 2015-01-29 22:06
author: Rubén Chavarría
comments: true
categories: 
- dart
published: true
footer: false
sidebar: true
---

[Dart] es un lenguaje de programación que se ejecuta en un único hilo. Si un
bloque de código bloquea dicho hilo (por ejemplo haciendo una operación de
entrada-salida de larga duración), la aplicación quedará *congelada*. Las
operaciones asíncronas permiten al programador crear operaciones sin bloquear
la aplicación entera. Dart usa la clase `Future` para realizar estas
operaciones asíncronas.

En el [tutorial sobre Futures] podrás encontrar información acerca de cómo
usar esta API de Dart.

<!-- more -->

## Introducción

El siguiente código haría que la aplicación quedara congelada:

```
import 'dart:io';

void printDailyNewsDigest() {
  File file = new File("dailyNewsDigest.txt");
  print(file.readAsStringSync());
}

void main() {
  printDailyNewsDigest();
  printWinningLotteryNumbers();
  printWeatherForecast();
  printBaseballScore();
}
```

El problema de este código es que `readAsStringSync()` no retorna hasta que no
termina, con lo que las llamadas al resto de métodos serán retrasadas. 

Para lograr hacer que esa llamada no bloquee la ejecución del resto, Dart proporciona
los *Futures*.

## ¿Qué es un *Future*?

Es simplemente un medio para obtener un valor en algún momento en el futuro. 

La forma en la que funciona es la siguiente: una función que necesita hacer una
acción muy costosa en el tiempo, encola dicha acción como un trabajo para hacer y
devuelve un objeto `Future` inmediatamente, de esta forma se consigue no bloquear
el hilo de ejecución de Dart. Más adelante, cuando el trabajo ha terminado, y el
valor está disponible, se dice que el `Future` se ha completado con dicho valor.

Para obtener el valor que representa `Future`, se usa el método `then()`, pasándole
como parámetro una función de callback que será llamada con el valor del `Future`.

## ¿Cómo se usa?

El método bloqueante anterior quedaría así usando `Future`:

```
import 'dart:io';
import 'dart:async';

void printDailyNewsDigest() {
  File file = new File("dailyNewsDigest.txt");
  Future future = file.readAsString();
  future.then((content) {
    print(content);
  });
}
```

Esta vez, para leer el fichero se usa el método `readAsString()`, el cual no bloquea
el hilo y retorna un `Future`. Después, se registra un callback a través del método
`then()`. Este callback recibe como parámetro el valor que esperamos que retorne
`readAsString()`, que es el contenido del fichero. Es en este callback donde
se imprime el contenido del fichero leído.

El propio método `then()` devuelve también un `Future`, por lo cual se pueden 
encadenar distintas llamadas `then()`.

## Gestión de errores

La gestión de errores con `Future` es muy sencilla, ya que la clase proporciona el
método `catchError()` que será llamado si se produce un error a la hora de conseguir
el valor que representa el `Future`.

El método anterior se puede reescribir así:

```
void printDailyNewsDigest() {
  File file = new File("dailyNewsDigest.txt");
  Future future = file.readAsString();
  future.then((content) => doSomethingWith(content))
        .catchError((e) => handleError(e));
}
```

De esta forma, si `readAsString()` produce un error, la variable `future` se completará
con error (en lugar de completarse con el valor del contenido del fichero), lo que
provocará que el `Future` devuelto por `then()` se complete también con error, lo que hará
que se llame al método `catchError()`, el cual gestionará el error.

## Encadenando múltiples llamadas a `then()`

Supongamos que existen tres funciones: `expensiveA()`, `expensiveB()` y `expensiveC()`. Todas
ellas devolviendo `Future`s, de forma que se pueden encadenar llamadas a `then()` de esta 
forma:

```
expensiveA().then((aValue) => expensiveB()) 
            .then((bValue) => expensiveC()) 
            .then((cValue) => doSomethingWith(cValue));
```

También existe otra posibilidad, y es esperar a que termine la ejecución de las tres, para
realizar alguna acción solamente cuando los tres `Future`s se hayan completado. Para ello,
el API proporciona el método `wait()`.

```
Future.wait([expensiveA(), expensiveB(), expensiveC()])
      .then((List responses) => chooseBestResponse(responses));
```

Aquí, `wait()` devuelve un `Future` cuyo valor es una lista con los valores de todos los
`Future`s pasados como parámetros.

## Creando tus propios `Future`

De acuerdo, entendido cómo se usan. Pero, ¿y si lo que quiero es ser yo quien comienza la
cadena de `Future`s? ¿Cómo se crea el primero de ellos?

```
Future methodReturningAFuture() {
    return new Future.value('foo bar');
}
```

El método del código anterior devuelve un valor, un `Future` que se resuelve al valor
`foo bar`. Si quisiéramos imprimir esa cadena por consola, haríamos lo siguiente:

```
methodReturningAFuture()
    .then((message) => print(message));
```

## Conclusión

Si así *en papel* no te ha quedado lo suficientemente claro, te recomiendo que te pases
por el [tutorial sobre Futures] o que le eches un ojo al [código completo] del tutorial.

[Dart]: http://dartlang.org
[tutorial sobre Futures]: https://www.dartlang.org/docs/tutorials/futures/
[código completo]: https://github.com/rchavarria/dart-tutorials/tree/master/futures

