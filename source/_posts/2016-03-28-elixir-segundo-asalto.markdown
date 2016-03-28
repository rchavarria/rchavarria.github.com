---
layout: post
title: "Elixir: segundo asalto"
date: 2016-03-27 17:42
author: Rubén Chavarría
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

Sigo aprendiendo [Elixir], despacio, pero sigo con ello. Éste es el segundo
asalto del aprendizaje. En este asalto, lucho con estructuras de datos un poco
más complejas, como listas, diccionarios, *structs* o *sets*. Estas estructuras
ya existen en otros lenguajes de programación, pero en Elixir son tratadas de
una forma un poco diferente.

Por supuesto, en este asalto también sigo el método de aprendizaje descrito
desde el post sobre [aprender Elixir]:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

{% img center /images/2016/rms-won.jpg %}

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/2PDNng">RMS won</a> de <a href="https://www.flickr.com/photos/kmerenkov/">Konstantin Merenkov</a>, <a href="https://creativecommons.org/licenses/by-nc/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by-nc/2.0/legalcode">CC BY-NC 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

**Listas**

Una lista es recursiva. Está formada por una cabecera (*head*) y una cola
(*tail*). La cabecera es unicamente el primer elemento. La cola, es una lista
con el resto de elementos. De esta forma, la lista `[1, 2, 3]`, en realidad es
`[1 | [2 | [3 | [] ] ] ]` (al final se concatena una lista vacía).

Como las listas son recursivas, muchas funciones que manipulan listas lo son.
Elixir hace super sencilla la recursividad. Mezclando recursividad y pattern
matching, se pueden hacer virgerías. Super fácil implementar el cifrado César
(ver [exercise-04-round-02.exs]).

**Diccionarios**

Existen varios tipos de diccionarios: `Maps`, `HashDicts`, `Keywords`, `Sets` y
`Structs`. 

Para acceder a una clave del diccionario: `dict[:key]`, las claves son Atoms.

`Enum.into` convierte entre tipos enumerados, por ejemplo, entre tipos de
diccionarios. 

```
#Distintas operaciones que podemos hacer sobre diccionarios
dict = %{ key1: "Clave 1", key2: "Clave 2" }%
ticd = %{ key9: "Clave 9", key8: "Clave 8" }%

# eliminar claves de un diccionario
Dict.drop(dict, [:key2])

# añadir claves
Dict.put(dict, :key3, "Clave 3")

# unir diccionarios
Dict.merge(dict, tcid)

# obtener valores, similar a dict[:key1]
Dict.get(dict, :key1)

# obtener todos los valores
Dict.values(dict)

# el pattern matching en diccionarios es muy útil
person = %{ name: "Dave", height: 1.88 }

# establecer a_name = "Dave"
%{ name: a_name } = person

# pattern matching que no falla
%{ name: _, height: _ } = person

# pattern matching que no falla
%{ name: "Dave" } = person

# falla
%{ name: _, weight: _ } = person
** (Match error) no ...

# pattern matching no puede enlazar claves de diccionarios
%{ 2 => state } = %{ 1 => ok:, 2 => error: }
=> state = :error

%{ state => ok: } = %{...}
=> Error ...

# para actualizar un mapa, se usa la siguiente estructura, muy parecida a `List`
# Puede actualizar pero no añadir
new_map = %{ old_map | key => value, ... }
```

**Mapas tipados (typed maps)**

Son como un mapa que tiene un conjunto de campos fijos y valores por defecto
para ellos. Se puede utilizar *pattern matching* por tipo y por contenido.

Estos mapas son los llamados `Struct`. Los `Struct`s son mapas limitados: las
claves deben ser *Atoms*. Se crean con `defstruct`, y el nombre del módulo pasa
a ser el nombre del struct:

```
defmodule Subscribrer do
  defstruct name: "", paid: false, over_18: true
end

s1 = %Subscribrer{}
=> %Subscribrer{ name: "", paid: false, over_18: true }

s2 = %Subscribrer{ name: "Dave" }

# a las claves se accede mediante un punto <struct>.<key>
s2.name
=> "Dave"

%Subscribrer{ name: name } = s2
name
=> "Dave"

# así se actualizan los datos
s3 = %Subscribrer{ s2 | name: "Marie" }

# la idea de que el nombre del módulo sea el nombre del Struct
# es que se puedan añadir métodos al módulo que modifiquen la
# estructura del Struct (esto me suena mucho a las clases de la
# Programación Orientada a Objetos).
defmodule Attendee do
  defstruct name: "", paid: false, over_18: true

  def may_attend_after_party(attendee = %Attendee{}) do
    attendee.paid && attendee.over_18
  end

  ...
end
```

El autor reconoce que los `Struct`s se parecen mucho a los objectos de la
Programación Orientada a Objetos. Y también nos advierte que tengamos cuidado,
que no caigamos en la tentación, que nos mantengamos puros, que no mezclemos
paradigmas.

**Estructuras de diccionario anidadas**

Las `Structs` se pueden anidar. Se consigue haciendo que el valor de una de las
claves sea otro `Struct`.

Imagina que tenemos dos `Struct`s anidadas así:

```
report = %BugReport{
  owner: %Customer{
    name: "Dave",
    company: "Pragmatic"
  },
  details: "broken"
}

# se puede acceder a company
company = report.owner.company

# podemos modificarla con la macro put_in
put_in(report.owner.company, "PragProg")
```

Con `update_in` podemos modificar el valor actual (accesible a través de un
parámetro de la macro). También existen las macros `get_in` y
`get_and_update_in`

Esas macros también funcionan con mapas y keyword lists. Si en lugar de una
clave o lista de claves, se pasa una función, las macros se convierten en
funciones dinámicas y llamarán a esta función con tres parámetros.

**Sets**

Actualmente solo hay una implementación de ellos, `HashSet`.

```
one_to_five = Enum.into 1..5, HashSet.new

# comprueba si un valor existe o no
Set.member(one_to_five, 5)
=> true

# concatena varios Set's
three_to_eight = Enum.into 3..8, HashSet.new
Set.union(one_to_five, three_to_eight)
=> #Hashset[ 1, 2, 3, 4, 5, 6, 7, 8]

# qué elementos estań en el primero que no están en el segundo
Set.difference(one_to_five, three_to_eight)
=> #Hashset[ 1, 2 ]
Set.difference(three_to_eight, one_to_five)
=> #Hashset[ 6, 7, 8 ]

# qué valores están en ambos
Set.intersection(one_to_five, three_to_eight)
=> #Hashset[ 3, 4, 5 ]
```

## Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas

Algunos métodos intersantes del módulo `List`: operadores para concatenar `++`,
diferencia `--`, pertenencia `in` y métodos tales como `flatten`, `foldl`,
`foldr`, `zip`, `unzip`, `keyfind`, `keydelete`, `keyreplace`,...

Además de los métodos que hemos visto de `Dict`, podemos encontrar: `values`,
`drop`, `put`, `merge`, `get`, `HashDict.new`,...

El módulo `Keyword` tiene métodos para manipular listas de tuplas, o keyword
lists: `delete`, `drop`, `equal?`, `get_and_update`, `merge`, `pop`, `put`,...

Existen unas macros, que sirven para manipular los valores almacenados en
diccionarios: `get_in`, `update_in`, `get_and_update_in`,... Si a estas macros
se les pasa una función en lugar de unas claves, se usará esa función para
obtener los valores del diccionario. Debería ser sencillo saber usarlas, pero
todavía no llego a entender exactamente cómo funciona y para qué se podría
utilizar.

## Aprender lo suficiente para hacer algo de utilidad

- [exercise-01-round-02.exs]: antes se ha implementado (en el libro) la
  funcción `sum`, que suma los elementos de una lista. Se ha utilizado un
  acumulador. Implementar lo mismo sin el acumulador
- [exercise-02-round-02.exs]: escribir una función `mapsum` que acepte una
  lista y una función, de forma que aplique la función a cada elemento y sume
  los resultados
- [exercise-03-round-02.exs]: escribir una función `max(list)` que devuelva el
  máximo valor de la lista
- [exercise-04-round-02.exs]: implementar el cifrado César, `caesar(list, n)`,
  donde `list` es una lista de carácteres (es decir, una cadena con comillas
  simples `'cadena'`) y que sea circular, cuando sobrepase `z`, que vuelva a la
  `a`.
- [exercise-05-round-02.exs]: escribir una función `span(from, to)` que
  devuelva una lista de números desde `from` hasta `to`.

## Enseñar lo aprendido

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[aprender Elixir]: /blog/2016/01/17/aprendiendo-elixir/
[exercise-01-round-02.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-02/exercise-01-round-02.exs
[exercise-02-round-02.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-02/exercise-02-round-02.exs
[exercise-03-round-02.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-02/exercise-03-round-02.exs
[exercise-04-round-02.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-02/exercise-04-round-02.exs
[exercise-05-round-02.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-02/exercise-05-round-02.exs

