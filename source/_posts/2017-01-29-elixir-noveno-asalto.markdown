---
layout: post
title: "Elixir: noveno asalto"
date: 2017-01-29 17:19
author: Ruben Chavarria
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

En el [asalto anterior] aprendimos un par de conceptos básicos sobre los nodos.
En este asalto aprenderemos sobre servidores OTP: qué son, para qué sirven, por
qué son útiles y cómo implementarlos fácilmente.

Todo esto, siguiendo el [método de aprendizaje] con el que comenzé la serie:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

{% img center /images/2017/us-air-force.jpg %}

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/R7mJ4M">160324-F-XK483-042</a> de <a href="https://www.flickr.com/photos/usairforce/">US Air Force</a>, <a href="https://creativecommons.org/licenses/by-nc/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by-nc/2.0/">CC BY NC 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

#### Servidores OTP

OTP (**O**pen **T**elecom **P**latform) se presenta como la solución a todos
tus problemas de escalabilidad y concurrencia. No es así, pero ayuda mucho.
Ayuda en temas como descubrimiento de aplicaciones, gestión y detección de
fallos, actualización de código en caliente y estructura del servidor.

OTP define un sistema como una jerarquía de **aplicaciones**. Una aplicación
consiste en uno o varios **procesos**. Cada uno de estos procesos implementa
un **comportamiento**. Existen [comportamientos] para servidores, gestores de
eventos, máquinas de estado finitas, ...

Lo implementado en ejercicios anteriores sigue un patrón con el que se podría
implementar casi todos los servidores. Por eso, OTP proporciona un mecanismo
para liberarnos de escribir el código más tedioso. La librería ofrece unas
funciones a modo de *callbacks* que irá llamando dependiendo de la situación.

#### Implementar un servidor OTP

```
defmodule Sequence.Server do
  use GenServer

  def handle_call(:next_number, _from, current_number) do
    { :reply, current_number, current_number + 1 }
  end

end
```

`use GenServer` indica a Elixir que vamos a usar este comportamiento. Así, este
módulo representa un servidor OTP.

Uno de los callbacks proporcionados por `GenServer` es `handle_call`. Tiene 3
parametros: acción, PID del origen de la petición y el estado actual del
servidor. Tiene que responder con una tupla con tres parámetros también: la
respuesta, el valor retornado y el estado del servidor a usar en la siguiente
llamada.

Para llamar a este servidor, entramos en `iex`. Arrancamos el servidor,
indicando el módulo y el estado inicial (similar a `spawn_link`).

```
promtp$ iex -S mix
iex> { :ok, pid } = GenServer.start_link(Sequence.Server, 100)
iex> GenServer.call(pid, :next_number)
100
iex> GenServer.call(pid, :next_number)
101
iex> GenServer.call(pid, :next_number)
102
```

#### Servidores que no tienen que devolver un resultado

En ocasiones no necesitamos que el servidor retorne un resultado. En estos
casos, para llamar al servidor emplearemos `GenServer.cast`, y para manejar
esas peticiones, nuestro servidor debe implementar el callback `handle_cast`.

#### Callbacks de GenServer

GenServer es un protocolo de OTP. OTP asume que este protocolo define 6
callbacks. Elixir proporciona una implementación por defecto para cada uno de
ellos en GenServer, por eso no tenemos que implementarlos nosotros. Los 6
callbacks son: `init(start_arguments)`, `handle_call(request, from, state)`,
`handle_cast(request, state)`, `handle_info(info, state)`,
`terminate(reason, state)`, `code_change(from_version, state, extra)` y
`format_status(reason, [ pdict, state ])`.

#### Nombrado de procesos

En lugar de usar el PID para referenciar a procesos de nuestro servidor,
podemos hacerlo a través de nombres. Para ello, se debe utilizar la opción
`name:` a la hora de crear el servidor:

```
iex> { :ok, pid } = GenServer.start_link(Sequence.Server, 100, name: :seq)
iex> GenServer.call(:seq, :next_number)
100
iex> GenServer.call(:seq, :next_number)
101
iex> GenServer.call(:seq, :next_number)
102
iex> :sys.get_status :seq
```

## Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas

## Aprender lo suficiente para hacer algo de utilidad

- [Ejercicio 01]: crear un server que implemente una pila. Se
inicializará con unos cuantos valores en la pila. Cada petición *pop*
devolverá un elemento de la pila. Cuando la pila esté vacía, fallará.
Implementado en el proyecto `mix`: `code/round-09/stack`.

- [Ejercicio 02]: ampliar el servidor anterior, de forma que se puedan
añadir elementos a la pila con la operación `:push` a través de peticiones
*cast*. Implementado en el proyecto `mix`: `code/round-09/stack2`.

- [Ejercicio 03]: dar un nombre al servidor anterior, de forma que se le
pueda llamar sin necesidad de saber el PID. También, crear un API en la pila
de forma que los clientes no tengan que llamar a `GenServer` para usarla.
Simplemente serán unas funciones que envolverán las llamadas a `GenServer`.
Implementado en otro proyecto `mix`, en `code/round-09/stack3`.

- Ejercicio 04: implementar el callback `GenServer.terminate/2` para
comprobar distintas formas de terminar el servidor: un callback lanza una
excepción, una llamada a `Kernel.exit/1`, se detecta que un proceso ha tenido
un error,...

**Resultado**

No he obtenido nada en claro. Tendría que profundizar en la documentación de
[`GenServer.terminate/2`](http://elixir-lang.org/docs/stable/elixir/GenServer.html#c:terminate/2),
que parece bastante espesa por cierto. Pero no está garantizado que se llame a
`terminate`, con lo que no sé si estoy provocando correctamente los errores.

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta
el siguiente asalto.

## Referencias

- Proceso de [aprendizaje de Elixir]
- Artículo sobre [comportamientos] (*behaviours*) en Elixir
- Artículo sobre [protocolos] en Elixir

[asalto anterior]: /blog/2016/12/31/elixir-octavo-asalto/
[método de aprendizaje]: /blog/2016/01/17/aprendiendo-elixir/
[aprendizaje de Elixir]: /blog/2016/01/17/aprendiendo-elixir/
[comportamientos]: http://rubenfa.github.io/2016-11-30-behaviours-en-elixir
[protocolos]: http://rubenfa.github.io/2017-01-25-protocols-en-elixir
[Ejercicio 01]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-09/stack
[Ejercicio 02]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-09/stack2
[Ejercicio 03]: https://github.com/rchavarria/learning-elixir/tree/master/code/round-09/stack3

