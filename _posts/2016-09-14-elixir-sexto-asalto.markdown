---
title: "Elixir: sexto asalto"
date: 2016-09-14 21:32
author: Ruben Chavarria
comments: true
categories: 
- elixir
- learning
published: true
footer: false
sidebar: true
---

Sexto asalto. En esta ocasión no veremos nada del lenguaje, si no del
ecosistema de [Elixir]. Elixir viene acompañado de unas magníficas herramientas
que complementan en lenguaje de programación en sí: `mix`, la herramienta de
construcción de aplicaciones y herramientas de testing como `ExUnit` y
`DocTests`. Además de estas herramientas, exploraremos también los sitios web
donde los desarrolladores alojan la mayoría de las librerías y proyectos Elixir
disponibles.

Sigo con la metodología de aprendizaje explicada en el [primer post sobre Elixir]:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

![Sixth]({{ site.baseurl }}/assets/images/2016/more-gladiators.png)

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/6xvcMz">More gladiators</a> de <a href="https://www.flickr.com/photos/archeon/">Hans Splinter</a>, <a href="https://creativecommons.org/licenses/by-nd/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

Elixir viene con la herramienta `mix`, la herramienta oficial de construcción
de proyectos (creación, testeo, construcción, gestión de dependencias,...). En
este asalto crearemos una aplicación que nos permitirá listar los últimos `n`
*issues* de cualquier proyecto de [GitHub].

`mix help` lista los comandos disponibles. Los más interesantes podrían ser:
`mix run` para ejecutar el proyecto, `mix test` para ejecutar los tests o `mix
new` para crear uno nuevo.

Crearemos un nuevo proyecto, llamado `rct_issues`:

```
$ mix new rct_issues
```

Listando los ficheros y directorios que ha creado el comando, encontramos los
siguientes:

- `/README.md`: aquí podemos poner la descripción del proyecto.
- `/config/`: donde vivirá la configuración del proyecto
- `/lib/`: aquí irá el código fuente de nuestro proyecto
- `/test/`: aquí irá el código de tests
- `mix.exs`: opciones de configuración del proyecto en sí

**Transformación: parsear la línea de comandos**

La aplicación de ejemplo tomará los parámetros de la línea de comandos. Las
aplicaciones Elixir consisten en una serie de transformaciones, y la primera de
ellas será la de parsear la línea de comandos.

En Elixir existen una serie de convenciones:

- El código que gestiona la línea de comandos va en un módulo llamado
  `<proyecto>.CLI`, así que nuestro código iría en un módulo llamado
`RctIssues.CLI`
- Cada módulo va en un fichero distinto
- Cada módulo va dentro del espacio de nombres del proyecto, por lo que todos
  los módulos colgarán de `RctIssues`
- Los *espacios de nombres* corresponden con directorios en el árbol del
  proyecto. Así, el módulo `RctIssues.CLI` se escribiría en el directorio
`/lib/rct_issues/cli.ex`. Ver fichero de código fuente [cli.ex]

**Los primeros tests**

Elixir viene con un pequeño framework de testing llamado `ExUnit`.

En el fichero `/test/cli_test.exs` escribiremos los tests para el módulo que
acabamos de escribir (echar un vistazo al fichero [cli_test.exs])

**Transformación: obtener datos de GitHub**

La siguiente transformación sería obtener datos de GitHub. Para ello
necesitaremos alguna librería externa. Hay varios lugares donde buscar:

1. Librerías propias de Eixir, en [http://elixir-lang.org/docs]
2. Librerías propias de Erlang (también distribuidas con Elixir), en
   [http://erlang.org/docs]
3. Si todo esto falla, podemos buscar en el repositorio de [Hex],
   el gestor de dependencias de Elixir
4. Si aún así, todo falla, siempre nos quedará Google y GitHub

El autor recomienda usar `HTTPoison` como librería. Esta librería se encuentra
en `Hex`, con lo que es muy fácil incluirla en nuestro proyecto. Simplemente
hay que modificar el método `deps` dentro del fichero `/mix.exs`, indicando el
nombre y la versión de la librería que queremos usar:

```
defp deps do
  [
    { :httpoison, "~> 0.4" }
  }
end
```

Con el comando `mix deps` podremos saber el estado de las dependencias del
proyecto. Con `mix deps.get` podremos descargar las dependencias que no estén
instaladas localmente. En caso de estar instaladas, lo estarán en el directorio
`/deps`, como proyectos Elixir, con lo que podremos navegar a través de ellas.

Ahora ya podemos usarla. Lo haremos en un nuevo módulo, escrito en
[`/lib/rct_issues/github_issues.ex`]. También modificaremos el método
`applications` de `mix.exs` para indicar que la dependencia `HTTPoison` va a
ser ejecutada como una *subaplicación* dentro de nuestro proyecto (hablará más
adelante sobre ello en el libro).

**Transformación: parsear la respuesta JSON**

Para la siguiente transformación incluiremos una dependencia que proviene del
mundo Erlang. `mix` es capaz de incluir dependencias de muy diversas fuentes,
Erlan entre ellas. Se añade la librería `jsx`, como dependencia del proyecto.
Añadir la línea `{ :jsx, "~> 2.0" }` al fichero `mix.exs` y ejecutar el comando
`mix deps.get` para instalarla localmente.

Modificaremos nuestro módulo que debe parsear la respuesta,
`lib/rct_issues/github_issues.ex`:

```
def handle_response(%{status_code: 200, body: body}) do
  { :ok, :jsx.decode(body) }
end          

def handle_response(%{status_code:   _, body: body}) do
  { :error, :jsx.decode(body) }
end          
```

**Configuración de la aplicación**

Cuando creamos el proyecto con `mix`, éste crea un directorio de configuración,
`config/`, con el fichero `config.exs`, donde podremos escribir ciertas
configuraciones de nuestro proyecto.
Cada línea de configuración suele ser un registro de clave valor, por ejemplo, para nuestro proyecto añadiríamos:

```
use Mix.Config
config :rct_issues, github_url: "https://api.github.com"
```

Más adelante, podremos usar este valor configurado gracias al módulo
`Application`, así

```
# crea una variable de clase llamada github_url
@github_url Application.get_env(:rct_issues, :github_url)
```

**Construir un ejecutable**

Para ello es necesario modificar el fichero `mix.exs`, para configurar la
herramienta `escript` y poder indicarle el módulo principal de la aplicación
que se va a construir, el cual debe de tener un método llamado `main`.

Para construir, simplemente ejecutar el comando:

```
mix escript.build
```

Y tendremos un ejecutable que podremos ejecutar como cualquier otra aplicación
de consola de Unix/Linux

**Ejecutando los comentarios**

¿Cómo? ¿Ejecutar los comentarios? No te preocupes, Elixir puede ejecutar
ciertos comentarios como si fueran tests. En realidad, ejecuta comentarios
escritos en cierta forma como si fueran sesiones de la herramienta `iex`. Esto
sí que es documentación ejecutable. Simplemente, espectacular.

Un comentario del tipo:

```
@doc """   
Given a list of rows, where each row contains a keyed list
of columns, return a list containing lists of the data in
each column. The `headers` parameter contains the
list of columns to extract

## Example 

    iex> list = [Enum.into([{"a", "1"},{"b", "2"},{"c", "3"}], HashDict.new),
    ...>         Enum.into([{"a", "4"},{"b", "5"},{"c", "6"}], HashDict.new)]

    iex> Issues.TableFormatter.split_into_columns(list, [ "a", "b", "c" ])
    [ ["1", "4"], ["2", "5"], ["3", "6"] ]
"""        
def split_into_columns(rows, headers) do
# ...
```

Creamos un nuevo fichero de tests en `test/doc_test.exs`:

```
defmodule DocTest do
  use ExUnit.Case
  doctest Issues.TableFormatter
end  
```

Donde `Issues.TableFormatter` es el módulo donde hemos incluido el comentario
*ejecutable*. Podemos lanzar los comentarios testeables con los comandos `mix
test test/doc_test.exs` o simplemente `mix test`.

Para crear la documentación del proyecto, está la herramienta ExDoc, similar a
JavaDoc. Para ello hay que añadirlo como dependencia del proyecto en el fichero
`mix.exs`:

```
defp deps do
[
# ...
  { :ex_doc, github: "elixir-lang/ex_doc" },
# ...
]
end
```

Para generarlos, instalar la dependencia con `mix deps.get`, y generar la
documentación con `mix docs`.

## Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas

- Necesitarás consular documentación sobre `OptionParser` para ser capaz de
  hacer el primer ejercicio... No solamente eso, si no que he escrito unos
tests para aprender cómo funciona [tests de exercise-01-round-06]
- ¿Como se hace para formatear una cadena siempre con la misma anchura?
  (¿`String.pad` o algo así?). Parece que [`String.ljust/3`] hace el trabajo.

## Aprender lo suficiente para hacer algo de utilidad

- [exercise-01-round-06]: repetir (honestamente) el proceso de crear un nuevo
  proyecto y crear un módulo que parsee opciones de la línea de comandos y un
test para ello
- [exercise-02-round-06]: seguir implementando el ejemplo del libro lo más
  honestamente que se pueda. Se implementarán las siguientes transformaciones:
obtener los datos de GitHub con HTTPoison, parsear el JSON resultante con JSX,
extraer sólo la información que nos interesa, ordenarla y recuperar sólo la
cantidad que quiere el usuario.
- [exercise-03-round-06]: implementar el resto de la funcionalidad de la
  aplicación
- [exercise-04-round-06]: escribir una aplicación que pida datos a un organismo
  de EEUU sobre el tiempo, parsee los datos XML y los muestre de forma
agradable

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta
el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[primer post sobre Elixir]: {{ site.baseurl }}{% post_url 2016-01-17-aprendiendo-elixir %}
[GitHub]: https://github.com
[cli.ex]: https://github.com/rchavarria/learning-elixir/blob/master/projects/rct_issues/lib/rct_issues/cli.ex
[cli_test.exs]: https://github.com/rchavarria/learning-elixir/blob/master/projects/rct_issues/test/cli_test.exs
[http://elixir-lang.org/docs]: http://elixir-lang.org/docs
[http://erlang.org/docs]: http://erlang.org/docs
[Hex]: http://hex.pm
[`/lib/rct_issues/github_issues.ex`]: https://github.com/rchavarria/learning-elixir/blob/master/projects/rct_issues/lib/rct_issues/github_issues.ex
[tests de exercise-01-round-06]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-06/exercise_01_round_06/test/option_parser_test.exs
[`String.ljust/3`]: http://elixir-lang.org/docs/stable/elixir/String.html#ljust/3
[exercise-01-round-06]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-06/exercise_01_round_06
[exercise-02-round-06]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-06/exercise_02_round_06
[exercise-03-round-06]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-06/exercise_03_round_06
[exercise-04-round-06]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-06/weather
