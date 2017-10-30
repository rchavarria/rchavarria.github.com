---
layout: post
title: "Elixir: undécimo asalto"
date: 2017-10-30 21:06
author: Ruben Chavarria
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

Nos acercamos al final y en este asalto aprenderemos qué son las [Aplicaciones
OTP], aunque en realidad ya hemos estado usando algunas. Aprenderemos cómo
`mix` facilita mucho la tarea y cómo esta herramienta nos permite empaquetar
nuestra aplicación para ser distribuida. Aprenderemos a definir el punto de
entrada de ejecución y cómo pasar parámetros iniciales. Las aplicaciones, junto
con los servidores y supervisores OTP hacen de este framework una herramienta
potentísima para desarrollar aplicaciones.

Todo esto, siguiendo el [método de aprendizaje] con el que comenzé la serie:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

{% img center /images/2017/fingers.jpg %}

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/9cXZUG">Asaltos</a> de <a href="https://www.flickr.com/photos/antoniobugarin/">Antonio Bugarin</a>, <a href="https://creativecommons.org/licenses/by/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

#### Aplicaciones OTP

Una *aplicación* en el mundo Elixir no es lo que normalmente conocemos como
tal. El término viene del mundo Erlang, y con *aplicación* se refieren más a lo
que comúnmente conocemos como componente, o servicio (¿microservicio podría
valer aquí?, probablemente). Una aplicación OTP en Elixir es como un servicio
del que puede depender de otros servicios, y que puede arrancar servidores y
supervisores.

Por lo general, las aplicaciones son dependencias de los programas que estamos
desarrollando. Pero otras aplicaciones residen en la parte más alta del árbol
de procesos, y éstas están diseñadas para ejecutarse directamente.

**El fichero de configuración de la aplicación**

La herramienta `mix` crea un fichero llamado `<tu-aplicacion>.app`. Este
fichero es la especificación de la aplicación, y contiene información que se
suele escribir en `mix.exs` e información de la compilación de nuestro código.
Cuando se lanza la aplicación, este fichero es consultado para saber cómo
cargarla y arrancarla.

**Creando una aplicación OTP**

En realidad ya hemos creado varias. Por ejemplo, el programa *Sequence*, de la
ronda anterior, lo ejecutábamos como si fuera una aplicación OTP. Cuando
creamos un nuevo proyecto con `mix`, éste añade un supervisor por defecto e
información en `mix.exs` para poder ejecutar el proyecto como una aplicación.
Más concretamente, `mix` crea la función `application`:

```
def application do
  [
    mod: { Sequence, [] }
  ]
end
```

El código anterior indica que el módulo principal se llama `Sequence`. OTP
asume que dicho módulo implementa una función llamada `start` (porque Elixir
define un *behaviour* `Application` que deben implementar las aplicaciones OTP
para ser consideradas como tal), a la cual le va a pasar el parámetro indicado
en la tupla (en este caso un array vacío). Si la tupla hubiera sido `{
Sequence, 1234 }` el parámetro pasado a la función `start` hubiera sido `1234`.

Esto es lo relativo a la opción `mod:`. Pero a la hora de configurar una
aplicación existe otra opción: `registered:`. Esta opción lista los nombres que
nuestra aplicación va a registrar. Podemos usar esto si queremos que dichos
nombres sean únicos entre todas las aplicaciones cargadas en el nodo o cluster:

```
def application do
  [
    mod: { Sequence, [] },
    registered: [
      Sequence.Server,
      "Any other name"
    ]
  ]
end
```

Ahora podemos ejecutar el comando `mix compile` para generar el fichero `.app`.
Este fichero se almacena en la ruta nada intuitiva de
`_build/dev/lib/sequence/ebin`. Este fichero define una tupla Erlang que define
la aplicación. `mix` ha añadido automáticamente los módulos de los que consta
la aplicación y las aplicaciones de las que depende, por ejemplo `kernel`,
`stdlib` o `elixir`.

A la hora de pasar parámetros de inicialización a las aplicaciones existe otra
posibilidad. La opción `env`, que acepta una lista de palabras clave (*keyword
list*)

```
def application do
  [
    mod: { Sequence, [] },
    env: [ initial_number: 12334 ],
    registered: [...]
  ]
end
```

Para después recuperar ese valor con `Application.get_env`:

```
defmodule Sequence do
  use Application
  def start(_type, _args) do
    initial_number = Application.get_env(:sequence, :initial_number)
    #...
```

## Aprender lo suficiente para hacer algo de utilidad

- [Ejercicio 1]: convierte tu servidor `Stack` en una aplicación OTP

- [Ejercicio 2]: hasta ahora no hemos testeado para nada ninguna aplicación.
  Mira a ver qué puedes hacer. Testear un server no parece algo muy sencillo,
no parece que se pueda ejecutar a la primera, porque el server debería estar
ejecutándose para poder *funcionar*. Pero Elixir está muy enfocado a los tests
automáticos, así que algo debe de existir.

**Resultados**

Y tanto que existe. Encontré el artículo [cómo se testea un `GenServer`], en la
documentación oficial: básicamente, en el *set up* de los tests, se levanta el
server. Luego, se puede llamar a la API del servidor tranquilamente. Al
parecer, si el proyecto está configurado como una aplicación, `mix` arranca la
aplicación, por lo que no hace falta levantar el server en el *set up*. Lo
malo, que no se puede inicializar con ningún valor de test.

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta
el siguiente asalto.

[Aplicaciones OTP]: https://elixir-lang.org/getting-started/mix-otp/supervisor-and-application.html
[Elixir]: http://elixir-lang.org/
[método de aprendizaje]: /blog/2016/01/17/aprendiendo-elixir/
[Ejercicio 1]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-11/stack
[Ejercicio 2]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-10/sequence
[cómo se testea un `GenServer`]: http://elixir-lang.org/getting-started/mix-otp/genserver.html#testing-a-genserver

