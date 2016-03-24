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

Sigo aprendiendo [Elixir], despacio, pero sigo con ello. Éste es el segundo asalto del aprendizaje. En este asalto, lucho con estructuras de datos un poco más complejas, como listas, diccionarios, *structs* o *sets*. Estas estructuras ya existen en otros lenguajes de programación, pero en Elixir son tratadas de una forma un poco diferente.

Por supuesto, en este asalto también sigo el método de aprendizaje descrito desde el post sobre [aprender Elixir]:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

## Aprender lo suficiente para comenzar

**Listas**

- Una lista es recursiva. Está formada por una cabecera (head) y una cola (tail). La cabecera es unicamente el primer elemento. La cola, es una lista con el resto de elementos. De esta forma, la lista `[1, 2, 3]`, en realidad es `[1 | [2 | [3 | [] ] ] ]` (al final se concatena una lista vacía).
- operadores sobre listas: `++` concatenar, `--` diferencia, `in` pertenencia
- como las listas son recursivas, muchas funciones que manipulan listas lo son. Elixir hace super sencilla la recursividad. Mezclando recursividad y pattern matching, se pueden hacer virgerías. Super fácil implementar el cifrado César (ver `MyList.exs`)

**Diccionarios**

- diccionarios: existen varios tipos: Maps, HashDicts, Keywords, Sets y Structs. ¿Cómo elegir el tipo correcto? El libro da las claves. 
- `Enum.into` convierte entre tipos enumerados, entre tipos de diccionarios. Para acceder a una clave del diccionario: `dict[:key]`, las claves son Atoms.
- `Dict.drop [:key, :key2]` elimina las claves del diccionario. `Dict.put` añade claves. `Dict.merge` une diccionarios. `Dict.get` es similar a `dict[:key]`. `Dict.get_values` devuelve todos los valores de una clave.
- pattern matching en diccionarios:

```
person = %{ name: "Dave", height: 1.88 }

# sets a_name = "Dave"
%{ name: a_name } = person

# doesn't fail
%{ name: _, height: _ } = person

# doesn't fail
%{ name: "Dave" } = person

# fails
%{ name: _, weight: _ } = person
** (Match error) no ...
```

- pattern matching no puede enlazar (bind) claves de diccionarios. `%{ 2 => state } = %{ 1 => ok:, 2 => error: }` funciona, pero `%{ state => ok: } = %{...}`
- para actualizar un mapa, se usa la siguiente estructura, muy parecida a `List`: `new_map = %{ old_map | key => value, ... }`. Puede actualizar pero no añadir

**Mapas tipados (typed maps)**

- también llamados estructuras
- *typed map*: un mapa que tiene un conjunto de campos fijos y valores por defecto para ellos, y puedes utilizar *patter matching* por tipo y por contenido. Eso es un `Struct`. Structs son mapas limitados: las claves deben ser Atoms. Y alguna cosa más. Se crean con `defstruct`, y el nombre del módulo pasa a ser el nombre del struct:

```
defmodule Subscribrer do
  defstruct name: "", paid: false, over_18: true
end

s1 = %Subscribrer{}
# %Subscribrer{ name: "", paid: false, over_18: true }

s2 = %Subscribrer{ name: "Dave" }
...

# A las claves se accede mediante un punto <struct>.<key>
s2.name
# "Dave"

%Subscribrer{ name: name } = s2
name
# "Dave"

# updates
s3 = %Subscribrer{ s2 | name: "Marie" }
```

La idea de que el nombre del módulo sea el nombre del Struct es que se puedan añadir métodos al módulo que modifiquen la estructura del Struct (esto me suena mogollón a las clases de la OOP)

```
defmodule Attendee do
  defstruct name: "", paid: false, over_18: true

  def may_attend_after_party(attendee = %Attendee{}) do
    attendee.paid && attendee.over_18
  end

  ...
end
```

- **Estructuras de diccionario anidadas**: las `Structs` se pueden anidar. Se consigue haciendo que el valor de una de las claves sea otro `Struct`
Imagina que tenemos dos `Struct`s anidadas así:

```
report = %BugReport{owner: %Customer{name: "Dave", company: "Pragmatic"}, details: "broken"}
```

- Podemos acceder a `company` así: `report.owner.company`.
- podemos modificar `company` con la macro `put_in`: `put_in(report.owner.company, "PragProg")`
- con `update_in` podemos modificar el valor actual (accesible a través de un parámetro de la macro). También existen las macros `get_in` y `get_and_update_in` (mirar documentación)
- esas macros también funcionan con mapas y keyword lists
- si en lugar de una clave o lista de claves, se pasa una función, las macros se convierten en funciones dinámicas y llamarán a esta función con tres parámetros

**Sets**

- **Sets**, actualmente solo hay una implementación de ellos, `HashSet`
- `Set.member?` nos dice si un valor está en el `Set` o no. 
- `Set.union` concatena `Set`s
- `Set.difference` devuelve los valores que están en el primer argumento pero no en el segundo
- `Set.intersection` devuelve los valores que están en ambos
- Al final del capítulo 8 reconoce que los `Struct`s se parecen mucho a los objectos de la OOP. Y también nos advierte que tengamos cuidado, que no caigamos en la tentación, que nos mantengamos puros, que no mezclemos paradigmas.

## Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas

- Mirar documentación del módulo `List`, tiene multitud de métodos útiles: `++`, `flatten`, `foldl`, `foldr`, `zip`, `unzip`, `keyfind`, `keydelete`, `keyreplace`,...
- Mirar documentación del módulo `Dict` (para manipular diccionarios): `values`, `drop`, `put`, `merge`, `get`, `HashDict.new`,...
- Mirar documentación del módulo `Keyword`, para manipular listas de tuplas, o keyword lists
- Juguetear, o ver documentación de las macros/funciones para manipular mapas y structs: `get_in`, `update_in`, `get_and_update_in`,...

## Aprender lo suficiente para hacer algo de utilidad

- exercise-01-round-02.exs: antes se ha implementado (en el libro) la funcción `sum`, que suma los elementos de una lista. Se ha utilizado un acumulador. Implementar lo mismo sin el acumulador
- exercise-02-round-02.exs: escribir una función `mapsum` que acepte una lista y una función, de forma que aplique la función a cada elemento y sume los resultados
- exercise-03-round-02.exs: escribir una función `max(list)` que devuelva el máximo valor de la lista
- exercise-04-round-02.exs: implementar el cifrado César, `caesar(list, n)`, donde `list` es una lista de carácteres (es decir, una cadena con comillas simples `'cadena'`) y que sea circular, cuando sobrepase `z`, que vuelva a la `a`.
- exercise-05-round-02.exs: escribir una función `span(from, to)` que devuelva una lista de números desde `from` hasta `to`.

## Enseñar lo aprendido

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta el siguiente asalto.

