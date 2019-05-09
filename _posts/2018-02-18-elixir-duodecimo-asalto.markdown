---
title: "Elixir: duodécimo asalto"
date: 2018-02-18 22:08
author: Ruben Chavarria
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

Este será el último asalto relativo a [Elixir] por ahora, y en él aprenderemos
qué son las [Tasks] y los [Agents], que se podrían traducir como *tareas* y
*agentes*. 

Éstas serán las dos últimas abstracciones de Elixir que vamos a estudiar. No
son de tan bajo nivel como las primitivas `spawn`, `send` y `receive` que vimos
en el [séptimo asalto] y tampoco son tan pesados como el [framework OTP].

Son un punto intermedio. Utilizan funcionalidades de OTP, pero nos aíslan de
muchos detalles, lo que hace que trabajar con procesos y procesos distribuidos
sea muchísimo más fácil.

![Twelveth]({{ site.baseurl }}/assets/images/2018/down-the-board.jpg)

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/majY5a">Down the board</a> de <a href="https://www.flickr.com/photos/erinthomaswilson/">Erin</a>, <a href="https://creativecommons.org/licenses/by-nc-nd/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by-nc-nd/2.0/">CC BY-NC-ND 2.0</a>
  </span>
</div>

<!-- more -->

Todo esto, siguiendo el [método de aprendizaje] con el que comenzé la serie:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

## Aprender lo suficiente para comenzar

#### Tareas

Una tarea o `Task` es una función que se ejecuta en segundo plano. Existen dos
funciones principales: `async` y `await` y su forma de usarla sería la
siguiente:

```
# ...
# Realizar una computación que tarde mucho tiempo
worker = Task.async(fn -> Fibonacci.of(200000) end)
# ...
# Obtener el valor devuelto por la función
result = Task.await(worker)
# ...
```

`async` crea un proceso separado que ejecuta la función. Devuelve un descriptor
del proceso o *worker*. `await` espera a que el proceso termine para recuperar
el valor devuelto por la función. En lugar de pasar una función, también
podemos pasar el nombre de un módulo, función y parámetros:
`Task.async(Fibonacci, :of, [ 200000 ])`.

Las `Task`s están implementadas como servidores OTP, por lo que podemos
incluirlas en nuestro árbol de supervisión de aplicaciones. Existen dos formas:

1. Pasando la función a ejecutar a `Task.start_link` en lugar de llamar a
   `Task.async` desde un proceso que ya esté supervisado
2. Creando un worker desde un supervisor:

```
import Supervisor.Spec
children = [
  worker(Task, [ fn -> do_something_extraordinary() end ])
]
supervise children, strategy: :one_for_one
```

#### Agentes

Un agente o `Agent` es un proceso también en segundo plano que mantiene un
estado. El estado puede ser accedido desde un proceso, nodo o múltiples nodos.

El estado inicial se toma desde una función que se le pasa a la hora de
arrancar el `Agent`.

Se utiliza `Agent.get` para obtener el estado. Hay que pasarle una función,
cuyo parámetro será el estado actual del `Agent`. El valor devuelto por
`Agent.get` es el valor devuelto por la función.

Se utiliza `Agent.update` para modificar el estado. También hay que pasar una
función. El valor devuelto por la función será el nuevo estado.

Veamos un ejemplo:

```
# count es el descriptor del Agent
iex> { :ok, count } = Agent.start(fn -> 0 end)
{:ok, #PID<0.69.0>}
iex> Agent.get(count, &(&1))
0            
# incrementa el en uno el estado
iex> Agent.update(count, &(&1+1))
:ok          
iex> Agent.update(count, &(&1+1))
:ok          
# obtiene el estado actual
iex> Agent.get(count, &(&1))
2
```

Los agentes son una abstracción especialmente pensada para almacenar el estado
de nuestros procesos. Por lo tanto, se recomienda no guardar el estado en
nuestros procesos, si no que los procesos que creemos nosotros usen un `Agent`
para almacenar. De esta forma, en caso de fallo en nuestro proceso, el estado
estará todavía disponible en el `Agent`, ya que es un proceso diferente al
nuestro.

[Elixir]: http://elixir-lang.org/
[Tasks]: https://hexdocs.pm/elixir/Task.html
[Agents]: https://hexdocs.pm/elixir/Agent.html
[séptimo asalto]: {{ site.baseurl }}{% post_url 2016-09-18-elixir-septimo-asalto %}
[framework OTP]: http://erlang.org/doc/
[método de aprendizaje]: {{ site.baseurl }}{% post_url 2016-01-17-aprendiendo-elixir %}
