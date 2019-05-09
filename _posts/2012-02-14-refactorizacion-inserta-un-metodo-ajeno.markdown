---
title: "Refactorización: inserta un método ajeno"
date: 2012-02-14 02:14
author: Rubén Chavarría
categories: 
- java
- software
- book reviews
comments: true
published: true
footer: false
sidebar: true
---

En este post voy a describir una de las muchas refactorizaciones que describe 
Martin Fowler en su libro 
[Refactoring: improving the design of existing code](http://martinfowler.com/refactoring/)
([mis impresiones sobre el libro]({{ site.baseurl }}{% post_url 2012-01-25-refactoring-improving-the-design-of-existing-code %})),
He escogido la refactorización de 
[insertar método ajeno](http://martinfowler.com/refactoring/catalog/introduceForeignMethod.html)
por ser una de las que, aun siendo sencilla, no había sido consciente de 
utilizarla hasta leer el libro.

<!-- more -->

<h3>Descripción</h3>

La refactorización consiste en crear un método en una clase (clase cliente) cuando en realidad ese método debería pertenecer a otra clase (clase servidor). De ahí el nombre de método ajeno (traducción libre de foreign method)

<h3>Por qué es necesaria</h3>

Esta refactorización aparece ante la necesidad de crear un método en la clase servidor, pero es imposible cambiar el código fuente de la misma.

<h3>Cómo llevar a cabo la refactorización</h3>

Lo primero es crear un método en la clase cliente que haga lo que necesitamos que haga la clase servidora. El primer parámetro de este método será un objeto de la clase servidora. En caso de necesitar algún parámetro más, éstos serían los parámetros en caso de que el método existiera en la clase servidora.

El objetivo de crear un nuevo método es el de poder reutilizar el código y evitar duplicidades. De esta forma podremos retutilizar el código del nuevo método, y en el caso de que en un futuro podamos cambiar el código fuente de la clase servidora, ese cambio será menos doloroso.

Martin Fowler aconseja comentar el método como `método ajeno`, para poder encontrar métodos candiatos a mover a sus clases correspondientes. En mi opinión, no creo que esto ayude demasiado a la hora de mantener el código, pero tampoco lo veo perjudicial. Así que aquí, que cada cual siga sus preferencias.

<h3>Código de ejemplo</h3>

Partimos del siguiente código de ejemplo, es un ejemplo muy sencillo pero espero que ilustre el caso lo suficientemente bien como para comprender la refactorización:

```
// ...
Date nextDay = new Date(previousDay.getYear(), 
                        previousDay.getMonth(), 
                        previousDay.getDate() + 1);
```

Como vemos, nuestro código necesita varios datos de la clase servidora (Date, objeto previousDay). Si la clase Date tuviera un método nextDay, o similar, nuestro código quedaría realmente simple. Pero no lo tiene, y lo pero de todo es que tampoco tenemos la posibilidad de modificar Date para incorporarle ese método.

Está bien, creemos pues nuestro método ajeno:

```
Date nextDay = nextDay(previousDay);
// ...
// foreign method
private Date nextDay(Date aDay) {
    return new Date(aDay.getYear(), 
                    aDay.getMonth(), 
                    aDay.getDate() + 1);
}
```

Sí, el código es prácticamente el mismo, pero ahora tenemos un método, la principal forma de reutilizar código. En el caso de poder modificar la clase Date, sería trivial mover este método a esa clase. De hecho, <a href="http://martinfowler.com/refactoring/catalog/moveMethod.html">mover método</a>, es una de las primeras refactorizaciones (y más básicas) explicadas por Martin Fowler en <a href="http://martinfowler.com/refactoring/">Refactoring</a>.