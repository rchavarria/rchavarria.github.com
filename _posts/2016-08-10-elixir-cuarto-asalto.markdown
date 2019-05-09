---
title: "Elixir: cuarto asalto"
date: 2016-08-10 17:20
author: Ruben Chavarria
comments: true
categories: 
- elixir
- learning
published: true
footer: false
sidebar: true
---

Éste es el cuarto asalto en mi aventura aprendiendo [Elixir]. En esta ocasión
trato con tipos de datos binarios, cadenas y **sigils**. No es mucho, pero las cadenas son
una parte esencial de cualquier lenguaje de programación. Y dominarlas
significa dominar una gran parte del lenguaje.

Por supuesto, sigo aprendiendo con el método descrito en el post sobre [aprender Elixir]:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

![Fourth fight]({{ site.baseurl }}/assets/images/2016/fourth-fight.jpg)

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/5yHK4Y">Muñeco de Gohan y Bu peleando</a> de <a href="https://www.flickr.com/photos/alotor/">Alonso Javier Torres</a>, <a href="https://creativecommons.org/licenses/by-nc/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

Para definir una cadena se pueden usar comillas simples o comillas dobles.
También se puede usar comillas triples, para escribir lo que llaman `heredocs`,
y se suelen usar para escribir comentarios para documentar métodos y módulos.

En Elixir, existe lo que llaman *sigils* (que se podría traducir como código,
señal o símbolo mágico). Comienzan con `~`, seguido de una letra que determina
el tipo de símbolo:

- `c` para una lista de carácteres
- `r` para expresión regular
- `w` para una lista de palabras separado por espacios
- y hay más

y cuyo valor se puede enmarcar en distintos delimitadores: `<..>`, `{...}`,
`[...]`,...

Un uso muy típico es para escribir expresiones regulares:

```
~r{[0-9]+[A-Z]*}
```

Los *sigils* pueden incluso personalizarse, y crear los tuyos propios.

Las cadenas definidas mediante comillas dobles, son lo que se conoce en otros
lenguajes como *strings*. Las cadenas con comillas simples, se llaman
*character lists* (o *char list*), listas de carácteres, y son listas, arrays.

**Cadenas con comillas simples**

Son una lista de códigos que representan los carácteres. Y como son una lista,
podemos usar métodos de `List`: `++`, `--`, `List.zip`, `[ head | tail ]`,...

Para saber el número entero que representa un carácter, se puede usar la
notación `?<chr>`, por ejemplo, `?a` o `?4`, para saber los valores numéricos
de los carácteres `a` y `4` respectivamente.

**Binarios**

Qué mejor que un poco de código para ver cómo se usa este tipo de datos

```
# el tipo *binario* representa una secuencia de bits
iex> b = << 1, 2, 3 >>
<<1, 2, 3>>
iex> byte_size b
3
iex> bit_size b
24

# se puede especificar también la cantidad de bits que queremos que ocupen
iex> b = << 1::size(2), 1::size(3) >>
<<9::size(5)>>
iex> byte_size b
1
iex> bit_size b
5

# también se pueden almacenar enteros, floats y otros binarios
iex> an_int = << 1 >>
<<1>>
iex> a_float = << 2.5 :: float >>
<<64, 4, 0, 0, 0, 0, 0, 0>>
iex> mix = << an_int :: binary, a_float :: binary >>
<<1, 64, 4, 0,......>>

# extraer valores (echa un vistazo a cómo se codifican los floats según
# el estándar IEEE 754)
iex> << sign::size(1), exp::size(11), mantissa::size(52) >> = << 3.14159::float >>
iex> (1 + mantissa / :math.pow(2, 52)) * :math.pow(2, exp-1023)
3.14159

# las cadenas con comillas dobles "" (dqs: double quoted string) son de
# tipo binario, y están codificadas en UTF-8 lo que significa que la
# longitud de la cadena no tiene por qué coincidir con el tamaño en bytes
iex> dqs = "∂x/∂y"
"∂x/∂y"
iex> String.length dqs
5
iex> byte_size dqs
9
```

**Procesando cadenas**

Igual que podemos dividir una lista en `head` y `tail`, podemos extraer el
primer carácter (se refiere a él como *grapheme*, grafema/grafo/...) de una
cadena binaria o *dqs* especificando que `head` es de tipo `utf8` y que `tail`
sigue siendo de tipo binario:

```
defp each(<< head::utf8, tail::binary >>), do [ head | each(tail) ]
defp each(<<>>), do []
```

## Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas

Está claro que hay que ver la documentación del módulo [`String`], que contiene
métodos para manipular cadenas encerradas en comillas dobles (recuerda, son de
tipo binario).

Las expresiones regulares son bastante comunes, y en Elixir se suelen usar
mediante [*sigils*]. Son un aspecto bastante curioso del lenguaje y pueden ser
personalizados.

## Aprender lo suficiente para hacer algo de utilidad

- [exercise-01-round-04.exs]: escribe una función que devuelva `true` si el
parámetro (una lista de carácteres) contiene sólo carácteres imprimibles (del
espacio a la tilde)
- [exercise-02-round-04.exs]: escribe una función que devuelva `true` en el
  caso de que dos palabras sean anagramas. `anagram?(word1, word2)`
- [exercise-03-round-04.exs]: escribe una funcion que calcule suma, resta,...
  de una cadena pasada como parámetro: `calculate('123 + 27') # => 150`. Este
  es especialmente difícil (al menos para mi nivel): devolver tuplas, parsear
  números (utilizando recursión de una forma muy imaginativa), utilizando pattern
  matching para construir funciones dependiendo del operador,...
- [exercise-04-round-04.exs]: escribe una función que pasándole una lista de
  dqs (double quoted strings) las imprima centradas en un ancho de la palabra
  más larga, cada una en una línea distinta.
- [exercise-05-round-04.exs]: escribe una función que pase a mayúsculas la
  primera letra de cada frase en una cadena
- [exercise-06-round-04.exs]: escribe una función que parsee un fichero CSV
  (que tendrá los campos id, estado y cantidad neta), y que se lo pase a la
  función desarrollada en el tercer asalto, al ejercicio
  `exercise-02-round-03.exs`.

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[aprender Elixir]: {{ site.baseurl }}{% post_url 2016-01-17-aprendiendo-elixir %}
[`String`]: http://elixir-lang.org/docs/stable/elixir/String.html
[*sigils*]: http://elixir-lang.org/getting-started/sigils.html
[exercise-01-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-04/exercise-01-round-04.exs
[exercise-02-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-04/exercise-02-round-04.exs
[exercise-03-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-04/exercise-03-round-04.exs
[exercise-04-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-04/exercise-04-round-04.exs
[exercise-05-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-04/exercise-05-round-04.exs
[exercise-06-round-04.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-04/exercise-06-round-04.exs

