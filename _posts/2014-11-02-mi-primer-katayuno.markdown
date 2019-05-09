---
title: "Mi primer katayuno"
date: 2014-11-02 01:14
author: Rubén Chavarría
comments: true
categories: 
- katayunos
- dart
- craftmanship
published: true
footer: false
sidebar: true
---

El pasado 25 de octubre asistí a un [katayuno] organizado por [Aprendiendo TDD].
Esta pequeña reunión tuvo lugar en [MateriaGris Coworking], un espacio de coworking
que ha montado un gran amigo mío.

El katayuno consistía en resolver un sencillísimo problema (el tema no es resolver
un gran problema sino practicar TDD): desarrollar un método que, tomando como parámetros
dos números enteros `a` y `b`, devuelva una lista con el doble de todos los números
impares entre ambos. Realizamos dos iteraciones, cada vez haciendo *pair programming*
con una pareja distinta.

En este post voy a describir cómo fueron mis dos iteraciones, y algo de código [Dart] que
he escrito después intentando simularlas, para poder ilustrar todo el proceso.

<!-- more -->

## Iteración 1

En este primera iteración seguimos unos pasos que a mí me parecían correctos.
Empezamos solucionando los casos más sencillos, como aquellos que el resultado
era una lista vacía por ejemplo, para terminar con los más complicados. Estos
pasos me parecían correctos, quizá porque estoy acostumbrado a resolverlos de
ese modo.

Más tarde, como vimos en la pequeña restrospectiva de la iteración mi pareja
y yo mostramos nuestro código, y criticaron bastante nuestro código, la verdad.
No es nada malo, de hecho, aprendimos bastante y otras parejas nos enseñaron
otro enfoque que me pareció interesante.

Al final de la iteración, nuestro código quedó más o menos así: 

```
class OddDoubler {
    List<int> compute(int a, int b) {
        List<int> list = new List<int>();

        while (a <= b) {
            if (isOdd(a)) {
                list.add(a * 2);
            }
            a++;
        }

        return list;
    }

    boolean isOdd(n) => n % 2 != 0;
}
```

El código completo, incluidos tests:
[iteración 1](https://github.com/rchavarria/katayuno-octubre-2014/blob/master/iteration-1/odd-doubles.dart).

A mí, personalmente, el código de producción me gusta, sencillo y
al grano. Pero para llegar a él, hay un paso, 
[donde introducimos el bucle while](https://github.com/rchavarria/katayuno-octubre-2014/commit/135d644fdbe75c5c8d6e17cd8f1461f7eaac67ce)
que quizá sea un paso demasiado grande, por lo que quizá los tests
elegidos no sean los más adecuados.

## Iteración 2

En esta segunda iteración cambiamos de pareja. Y también cambiamos la forma
de atacar el problema. Esta vez, siguiendo los consejos de los compañeros
de la iteración anterior, decidimos resolver el problema avanzando por
estados intermedios. Así que esta vez, no solucionamos el problema
desde los casos más sencillos hasta los más complicados.

Decidimos que los pasos intermedios serían:

- Decidir si un número is impar o no
- Implementar un método que nos diera una lista de todos los números entre
dos números dados
- Implementar un método que nos eliminara de una lista los números pares
- Implementar un método que multiplicara por 2 todos los elementos de
una lista

No llegamos a completarlo del todo, la iteración se nos quedó corta, pero
la idea la implementé más tarde y éste es el resultado de la
segunda iteración:

```
class OddDoubler {
    boolean isOdd(int n) => n % 2 != 0;

    List<int> getNumbers(int a, int b) => new List<int>.generate((b - a + 1), (int index) => a + index);

    List<int> filterOdds(List<int> numbers) {
        numbers.removeWhere((n) => !isOdd(n));
        return numbers;
    }
    
    List<int> doubleNumbers(List<int> numbers) => numbers.map((n) => n * 2);

    // This method should be the only public method
    // It resolves the KATA
    List<int> compute(int a, int b) => doubleNumbers(filterOdds(getNumbers(a, b)));
}
```

El código completo, incluidos tests:
[iteración 2](https://github.com/rchavarria/katayuno-octubre-2014/blob/master/iteration-2/odd-doubles.dart).

Me gusta más la aproximación de esta iteración, pero lo que no me gusta
es que hay métodos públicos que en realidad deberían ser privados. Son
públicos porque hemos creado tests para comprobar su funcionamiento, pero
deberían ser privados porque no aportan nada fuera de la implementación
de la clase. 

Como todo en el desarrollo del software, toda decisión tiene su parte
buena y su parte no tan buena.

## Conclusión

Es la primera vez que participo en un evento de este tipo, y espero que no
sea la última. La experiencia me encantó.

Sí, es cierto, en la primera iteración nos dieron bastante caña a mi pareja
y a mí, pero eso nos sirvió para entender que no todas las aproximaciones son
igual de buenas, y que hay que ser humilde para tener la mente abierta y
poder aprender de los demás compañeros.

Este tipo de eventos nos ayudan a ser mejores profesionales, y era mi objetivo
al participar en él. Gracias a [Aprendiendo TDD] y a [MateriaGris Coworking]
creo que todos aprendimos algo aquella mañana.

Gracias chicos.

[katayuno]: http://katayunos.com
[Aprendiendo TDD]: http://aprendiendotdd.com
[MateriaGris Coworking]: http://www.materiagriscoworking.com
[Dart]: http://dartlang.org
