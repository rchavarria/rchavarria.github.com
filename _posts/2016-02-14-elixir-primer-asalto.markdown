---
title: "Elixir: primer asalto"
date: 2016-02-09 21:57
author: Rubén Chavarría
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

Éste es el primer asalto de mi aprendizaje de [Elixir]. En él, no espero
resolver problemas súper complicados, es un primer contacto con el lenguaje. Me
conformaré con ser capaz de escribir un programa algo más complicado que un
simple hola mundo. En este primer asalto, lucho con tipos de datos, funciones
(anónimas y con nombre), pattern matching, claúsulas de guarda y módulos.

En estos asaltos, intentaré seguir los siguientes pasos:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

![Touch gloves]({{ site.baseurl }}/assets/images/2016/touch-gloves-derived-small.png)

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/awy1vc">Touch Gloves</a> de <a href="https://www.flickr.com/photos/kaiban/">Jack Zallum</a>, <a href="https://creativecommons.org/licenses/by-nc/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by-nc/2.0/legalcode">CC BY-NC 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

**Instalación**

Instalar la máquina virtual de Erlang y el entorno de Elixir es extremadamente
sencillo. Aquí están los comandos para hacerlo en una máquina con Ubuntu como
sistema operativo. En la [documentación de Elixir] hay instrucciones para otros
sistemas operativos.

```
$ wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
$ sudo dpkg -i erlang-solutions_1.0_all.deb
$ sudo apt-get update
$ sudo apt-get install esl-erlang
$ sudo apt-get install elixir
```

**Editores**

La comunidad de Elixir ha creado plugins para los editores de código más
famosos, entre ellos [Vim], que utilizo para mis [proyectos personales].

Instalar el plugin [vim-elixir] en Vim es facilísimo si instalas plugins con
pathogen:

```
$ git clone https://github.com/elixir-lang/vim-elixir.git ~/.vim/bundle/vim-elixir
```

**Herramientas**

`iex` es una herramienta de tipo REPL (read, evaluate, print, loop), que nos
permite ejecutar código Elixir de forma rápida. El comando `iex <fichero.exs>`
compila un script de Elixir y lo carga en la herramienta. Si ya estamos dentro
de ella, el comando para compilar el código Elixir de un fichero sería `c
"<fichero exs>"`.

**Pattern matching**

El operador `=` es muy diferente a lo que esperamos de él los que estamos
acostumbrados a la programación orientada a objetos. Tiene una apariencia
similar, pero no se comporta de la misma forma. Con este operador, Elixir trata
de hacer coincidir los valores de la izquierda con los valores de la derecha.

```
a = 2
[a, b, a] = [1, 2, 1]
[^a, b] = [2, 3]
[a, b, c] = [1, 2, [3, 4, 5]]   # c vale [3, 4, 5]
```

**Inmutabilidad**

¿Es eficiente devolver una copia de los datos? En los lenguajes funcionales, no
se modifican los datos, se devuelve una copia de ellos transformados. Parece
ineficiente, pero es todo lo contrario. Al no modificarse los originales, éstos
pueden compartirse por muchas variables, y pueden estar tranquilos, ya que no
se va a modificar. En los lenguajes no funcionales, se devuelve una copia (no
eficiente), en los funcionales, en realidad no se devuelve una copia, se
comparte todo lo que se puede. Por lo que es más eficiente.

¿Qué pasa con el recolector de basura? ¿Consume muchos recursos para deshacerse
de todos esos datos transformados que ya no se utilizan? No consume mucho, en
Elixir (en Erlang en realidad), hay muchos procesos, cada uno con un *heap*
distinto, por lo que el heap es más pequeño que en otros lenguajes, y el
recolector de basura se ejecuta bastante más rápido.

**Tipos de datos**

Y por fin algo de código:

```
# enteros
this_is_an_int = 1234
this_is_an_int = 0xcafe    # admite hexadecimal
this_is_an_int = 0o765     # octal
this_is_an_int = 0b01010   # binario
this_is_an_int = 1_000_000

# en coma flotante
this_is_a_float = 1.0
this_is_a_float = 0.245
this_is_a_float = .342        # error
this_is_a_float = 314159.0e-5

# rangos
this_is_a_range = 1..100

# expresiones regulares
this_is_a_regexp = ~r{regexp}options

# tuplas
this_is_a_tuple = { :ok, 42, "next" }

# listas: se parecen a los arrays de otros lenguajes, pero no
#lo son. Son estructuras enlazadas. Una lista o está vacía, o
#contiene un head y un tail, donde tail es otra lista
this_is_a_list = [ 1, 2, 3 ]

# mapas: lista de parejas clave/valor 
this_is_a_map = %{ key => value, key => value }
# si las claves son Atoms, se puede escribir
this_is_a_map = %{ red: 0xFF0000, green: 0x00FF00, blue: 0x0000FF }

# binarios: para acceder a datos como una secuencia de bits y bytes (para muy bajo nivel)
```

Hay otros tipos de datos, como los PIDs (referencias a procesos locales o
remotos) o los puertos (referencias a recursos sobre los cuales leeremos o
escribiremos).

Un tipo de datos muy interesante (y que yo personalmente no conocía) son los
*Atoms*: constantes representando el nombre de algo. Su nombre es su valor. Dos
Atoms son igules si tienen el mismo nombre, vengan de donde vengan (incluso de
máquinas diferentes)

```
# atoms
this_is_an_atom = :fred
this_is_an_atom = :is_binary?
this_is_an_atom = :var@32
this_is_an_atom = :<>
this_is_an_atom = :"lo john silver"
```

Hay dos estructuras muy similares, la lista de palabras clave: `[red: 0xFF000,
green: 0x00FF00]`, que se transforma en `[{:red, 0xFF0000}, {:green,
0x00FF00}]` y un mapa `%{red: 0xFF000, green: 0x00FF00}`. Se recomienda usar la
lista de palabras clave para pasar parámetros y usar los mapas cuando se
necesite un array asociativo.

No hemos dicho nada de las cadenas. Pertenecen al tipo *Binario*. Existe
interpolación de cadenas, con `#{...}` se evalúa el código de dentro y se
formatea la cadena con el valor obtenido.

**Funciones anónimas**

```
sum = fn (a, b) -> a + b end
sum.(2, 3)   # devuelve 5
```

Las funciones pueden devolver otras funciones. Las funciones recuerdan su
entorno original. Forman lo que se conoce como *closures*. Me recuerda mucho a
las funciones de JavaScript en este aspecto.

Existe una forma de crear funciones anónimas de una forma muy concisa, con el
operador `&...`

```
sum = fn (a, b) -> a + b end
sum2 = &(&1 + &2)   # idéntica a la función anterior

# devuelve lista con dos elementos: doble del primer parámetro, y cuadrado del mismo
returns_a_list = &[2 * &1, &1 * &1]

# esta notación viene muy bien para pasar funciones por parámetro
Enum.map [1, 2, 3] &(&1 * &1)   # devuelve [1, 4, 9]
```

Es normal ver la definición de una función como `&map/2`, donde `map` es el
nombre de la función y `2` es el *arity*, el número de parámetros de la misma.

**Módulos, funciones con nombre y funciones privadas**

```
defmodule Times do
  ## define una función en una única línea
  def double(n), do: n * 2

  ## define una función en varias líneas
  def triple(n) do
    n * 3
  end

  ## define una función privada
  defp quadruple(n), do: n * 4
end
```

Las funciones con nombre pueden tener varios cuerpos. Eso ayuda a utilizar
*pattern matching* a la hora de implementar una solución.

```
defmodule Factorial do
  # el factorial de 0, siempre es 1, esta definición es quien para la recursividad
  def of(0), do: 1

  # el factorial de cualquier otro número, es recursivo
  def of(n), do: n * of(n - 1)
end

Factor.of(5)
  # => 120
```

También, las definiciones pueden tener claúsulas de guarda, mediante 
`when <condition>`, lo que ayuda a tener un pattern matching más específico.

```
defmodule Guard do
  def what_is(x) when is_number(x) do
    IO.puts "#{x} is a number"
  end
  def what_is(x) when is_list(x) do
    IO.puts "#{x} is a list"
  end
  def what_is(x) when is_atom(x) do
    IO.puts "#{x} is an atom"
  end
end
```

**El operador tubería (pipe)**

El operador `|>` toma el resultado de una función y lo pasa como primer
parámetro de la segunda función. `String.reverse "foobar" |> String.capitalize`

```
filing = DB.find_customers
           |> Orders.for_customers
           |> sales_tax(2016)
           |> prepare_filing
      
list
  |> sales_taxes(2016)
  |> prepare_filing

# es lo mismo que llamar
prepare_filing( sales_taxes(list, 2016) )
```

**Parámetros por defecto**

```
defmodule DefaultParams do
  def func(p1, p2 \\ 2) do
    IO.inspect [p1, p2]
  end
end

Example.func("a", "b")
  # => ["a", "b"]

Example.func("a")
  # => ["a", 2]
```

**Librerías**

Se pueden buscar módulos y librerías ya implementados para realizar ciertas
tareas que necesitemos, para ello, está la documentación de [librerías de Elixir].
Si no encontramos ahí lo que buscamos, lo podemos buscar en [librerías de Erlang].

## Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas

**¿Qué hace `^` en el pattern matching?**

El operador `^` obliga a que el valor actual de una variable coincida con el
valor en la expresión de *pattern matching*. En caso de no coincidir, se
producirá un error.

```
a = 2
[^a, b] = [2, 3]  ## no hay error, `a` valía `2` y aquí coinciden
[^a, b] = [1, 3]  ## error
```

**Tuplas, *keyword list* y mapas**

Las *keyword list* son una lista usadas muy a menudo, tienen la forma:

```
keyword_list = [ red: 0xFF0000, green: 0x00FF00, blue: 0x0000FF ]
```

Pero no es más que una forma simplificada de escribir una lista de tuplas,
donde el primer valor de cada una de ellas es un Atom:

```
tuple_list = [ {:red, 0xFF000}, {:green, 0x00FF00}, {:blue, 0x0000FF} ]
```

Una estructura muy parecida a estas son los mapas, que no son más que un
conjunto de parejas clave-valor: 

```
a_map = %{ :red => 0xFF000, :green => 0x00FF00, :blue => 0x0000FF }
```

## Aprender lo suficiente para hacer algo de utilidad

- [round-01-exercise-01.exs]: utilizar varios cuerpos de una función y
  recursividad para implementar una función que calcule la suma de `1` hasta
`n`
- [round-01-exercise-02.exs]: implementar la función `gcd(x, y)` que calcule el
  máximo común divisor. Matemáticamente: `gcd(x, y)` es `x` si `y` es cero y es
`gcd(y, rem(x, y))` en caso contrario
- [round-01-exercise-03.exs]: crear el juego *Estoy pensando en un número entre
  el 1 y el 100*: rangos, div(a, b), claúsulas de guarda, pattern matching en
rangos: `a..b = 4..8`, funciones privadas

## Enseñar lo aprendido

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[documentación de Elixir]: http://elixir-lang.org/install.html
[Vim]: http://www.vim.org/
[proyectos personales]: http://rchavarria.github.io/pet-projects/
[vim-elixir]: https://github.com/elixir-lang/vim-elixir
[librerías de Elixir]: http://elixir-lang.org/docs.html
[librerías de Erlang]: http://erlang.org/doc/
[round-01-exercise-01.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-01/round-01-exercise-01.exs
[round-01-exercise-02.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-01/round-01-exercise-02.exs
[round-01-exercise-03.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-01/round-01-exercise-03.exs
