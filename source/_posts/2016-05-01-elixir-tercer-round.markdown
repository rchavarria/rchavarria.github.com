---
layout: post
title: "Elixir: tercer asalto"
date: 2016-05-01 17:46
author: Ruben Chavarria
comments: true
categories: 
- elixir
- learning
published: true
footer: false
sidebar: true
---

Éste es el tercer asalto para aprender [Elixir], y las cosas se van poniendo
interesantes, aunque todavía siento que estoy muy verde y me falta todavía
mucho para ser capaz de hacer las cosas más sencillas.

En este asalto, aprendo nuevas cosas proporcionadas por los módulos `Enum`,
`Stream` y otras coleciones, así como las *comprehensions*, que me recuerdan
mucho a los clásicos bucles `for`.

Sigo aprendiendo siguiendo el método descrito en el post sobre [aprender Elixir]:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

{% img right /images/2016/third-fight.png %}

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/c9bWJA">3rd fight</a> de <a href="https://www.flickr.com/photos/takfoto/">Tomasz Krawczak</a>, <a href="https://creativecommons.org/licenses/by-nc/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by-nc/2.0/legalcode">CC BY-NC 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

**Procesando colleciones con `Enum`**

Elixir tiene muchos tipos de datos que actúan como colleciones: listas, mapas,
diccionarios, rangos, ficheros e incluso funciones. Las colecciones se pueden
iterar (sobretodo con funciones del módulo `Enum`), y algunas permiten añadir
elementos.

```
# convierte cualquier colección a List
list = Enum.to_list 1..5
  #=> [1, 2, 3, 4, 5]

# concatena
Enum.concat([1, 2, 3], [4, 5, 6])
  #=> [1, 2, 3, 4, 5]

# crea nuevas colleciones
Enum.map(list, &(&1 * 10))
  #=> [10, 20, 30, 40, 50]

# selecciona elementos por posición
Enum.at(10..20, 3) #=> 13
Enum.at(10..20, 20) #=> nil
Enum.filter(list, &(&1 > 2)) #=> [3, 4, 5]
Enum.reject(list, &Integer.is_even/1) #=> [1, 3, 5]

# ordena y compara elementos
Enum.sort([ "there", "was", "a", "crooked", "man" ], 
  &(String.length(&1) <= String.length(&2))
Enum.max([ "there", "was", "a", "crooked", "man" ]) #=> "was"

# divide una colleción
Enum.take(list, 3)    #=> [1, 2, 3]
Enum.take_every(list, 2)  #=> [1, 3, 5]
Enum.take_while(list, &(&1 < 4))
Enum.split(list, 3)
  #=> { [1, 2, 3], [4, 5] }
Enum.split_while(list, &(&1 < 4))
  #=> { [1, 2, 3], [4, 5] }

# une los elementos de una colección
Enum.join(list)
Enum.join(list, ", ")   #=> "1, 2, 3, 4, 5"

# hace preguntas sobre operaciones
Enum.all?(list, &(&1 < 4))
Enum.any?(list, &(&1 < 4))
Enum.member?(list, 4)
Enum.empty?(list)

# mezcla colecciones
Enum.zip(list, [:a, :b, :c])
  #=> [ {1, :a}, {2, :b}, {3, :c} ]

# otros
Enum.reduce(<collection>, <function>)
```

**`Stream`s, enumerables diferidos o perezosos**

El módulo `Stream` permite enumerar collecciones de forma diferida (*lazy* es
la palabra utilizada, que traduzco libremente como *diferida*).

Las funciones del módulo `Enum` procesan todos los elementos de la colección de
una vez, consumiendo memoria. Las del módulo `Stream` consumen los elementos de
uno en uno, según se van necesitando. Los *streams* se pueden componer, es
decir, los streams son collecciones, por lo que se pueden usar las funciones de
`Stream` con los propios streams (sería como crear streams de streams).

Finalmente, para obtener los resultados, se puede convertir un `Stream` a una
lista:

```
[1, 2, 3, 4, 5]
  |> Stream.map(&(&1 * &1)
  |> Stream.map(&(&1 + 1)
  |> Stream.filter(fn x -> rem(x, 2) == 1 end)
  |> Enum.to_list
```

Con `Enum` debemos esperar a tener todos los elementos de la colección para
empezar a procesarlos. Con `Stream` podemos comenzar a procesarlos
inmediatamente. Imagina que leemos de un servidor remoto, o de un sensor, ambos
mandan datos infinitamente, por lo que `Enum` no sería una opción válida en
este caso.

Normalmente, serán las librerías y los frameworks quienes nos proporcionen los
streams con los que vamos a trabajar, pero también podemos crearlos nosotros
con métodos proporcionados por Elixir: `cycle`, `repeatedly`, `iterate`,
`unfold` y `resource`.

```
# cycle toma una coleción y va devolviendo de uno en uno indefinidamente
#cuando la colección se acaba, vuelve a empezar desde el principio
Stream.cycle([1, 2, 3])
  |> Enum.take(10)
#=> [1, 2, 3, 1, 2, 3, 1, 2, 3, 1]

# repeatedly toma una función y la ejecuta cada vez que se le pide un elemento
Stream.repeatedly(fn -> true end) |> Enum.take(3)
  #=> [ true, true, true ]
Stream.repeatedly(&:random.uniform/0) |> Enum.take(3)
  #=> [ 0.723, 0.941, 0.1234 ]

# iterate toma un valor inicial y una función. el primer elemento es el valor inicial,
#el siguiente es el valor devuelto por la función pasándole el valor inicial, el siguiente
#es el valor devuelto por la función pasándole el valor anterior, así indefinidamente
Stream.iterate(0, &(&1 + 1)) |> Enum.take(5)
  #=> [0, 1, 2, 3, 4]

# unfold es similar a iterate, pero con tuplas. el primer valor de la tupla
#significa el valor de la iteración actual, el segundo valor significa el valor
#a procesar en la siguiente iteración
Stream.unfold( {0, 1}, fn {f1, f2} -> {f1, {f2, f1+f2}} end ) |> Enum.take(15)
  #=> [0, 1, 1, 2, 3, 5, 8, 13, ... fibonacci]

# resource es similar a unfold. toma tres funciones como argumentos. la primera
#crea el recurso, la segunda va dando valores de las iteraciones (como unfold)
#y la tercera cierra el recurso (fichero, bbdd, ...)
```

**El protocolo `Collectable`**

No son lo mismo, y todavía no soy capaz de describir exactamente lo que es un
*protocolo*, pero el concepto que tengo de ellos hoy mismo es que son
*equivalentes* a las interfaces en los lenguajes orientados a objetos.

`Enumerable` es un protocolo que permite iterar una colección. `Collectable`
permite añadir elementos a una colección. Se puede utilizar `Enum.into` para
hacerlo y convertir un tipo de colección en otro.

```
Enum.into 1..5, [1000, 10001]
  #=> [1000, 1001, 1, 2, 3, 4, 5]
```

**Comprehensions**

Se le pueden pasar una o más colecciones, entonces extrae todas las
combinaciones posibles de los elementos de dichas colecciones, opcionalmente
puede filtrar valores, y genera una nueva colección con los valores que pasan
el filtro. La sintaxis es `result = for <generator> or <filter>, do:
<expression>`. Donde `<generator>` tiene la forma `pattern <- collection` y el
filtro es simplemente una condición, por ejemplo `x < 4`.

Las variables declaradas en una comprehension tienen la misma como ámbito, no
escapan de él.

```
for x <- [1, 2, 3, 4, 5], x < 4, do: x * x
  # => [1, 4, 9]

for x <- [1, 2], y <- [5, 6], do: x * y
  # => las posibles combinaciones serían [1, 5], [1, 6], [2, 5], [2, 6]
  # => y esas combinaciones serían las iteraciones de la comprehension

# se pueden usar variables de generadores en siguientes generadores
min_maxes = [ {1, 4}, {2, 3}, {10, 15} ]
for { min, max } <- min_maxes, n <- min..max, do: n
  # => [ 1, 2, 3, 4, 2, 3, 10, 11, 12, 13, 14, 15 ]

# por defecto, las comprehensions devuelven una lista. Se puede cambiar
# con el parámetro `into:`
for x <- ~w{ cat dog }, into: Map.new, do: { x, String.upcase(x) }
  # => %{ "cat" => "CAT", "dog" => "DOG" }
```

## Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas

Podría investigar sobre qué son los protocolos, pero creo que están descritos
en el libro del cual está surgiendo esta serie de posts, por lo que esperaré a
llegar ahí.

Tener siempre muy presente las funciones del módulo `Enum`, ya que casi seguro
que se van a utilizar siempre que haya colecciones de por medio.

## Aprender lo suficiente para hacer algo de utilidad

- [exercise-01-round-03.exs]: con ayuda de la función `span` escrita anteriormente, escribir una función que devuelva la lista de números primos de `2` hasta `n`
- [exercise-02-round-03.exs]: a partir de dos listas, una de tasas de impuestos, y otra de compras, calcular el importe total de cada una de las compras
- [lists-and-recursion-5.exs]: implementar funciones presentes en `Enum`: `all?`, `each`, `filter`, `take` y `split`.
- [lists-and-recursion-6.exs]: implementar `flatten`

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[aprender Elixir]: /blog/2016/01/17/aprendiendo-elixir/
[exercise-01-round-03.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-03/exercise-01-round-03.exs
[exercise-02-round-03.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-03/exercise-02-round-03.exs
[lists-and-recursion-5.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-03/lists-and-recursion-5.exs
[lists-and-recursion-6.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-03/lists-and-recursion-6.exs

