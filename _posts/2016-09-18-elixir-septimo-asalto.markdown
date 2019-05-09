---
title: "Elixir: séptimo asalto"
date: 2016-09-18 16:20
author: Ruben Chavarria
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

El aprendizaje va avanzando, ya vamos por el séptimo asalto. Éste trata sobre
cómo [Elixir] maneja múltiples procesos, por lo que trataremos algún tema de
concurrencia. También veremos algunas cosas básicas sobre cómo monitorizar los
procesos de los que consta nuestra aplicación.

Sin olvidar del método de aprendizaje con el que [comenzé]:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

![Seventh]({{ site.baseurl }}/assets/images/2016/you-gotta-fight-for-your-right-to-eat.jpg)

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/4rvPED">You gotta fight for your right to... eat</a> de <a href="https://www.flickr.com/photos/r2wk/">ldjpg</a>, <a href="https://creativecommons.org/licenses/by-nc-nd/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by-nc-nd/2.0/">CC BY NC ND 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

**Trabajando con múltiples procesos**

Elixir usa el [modelo de actores] para gestionar la concurrencia.

Elixir se apoya en Erlang para gestionar los procesos, que no son los procesos
del sistema operativo.

Para crear un proceso, se hace con la llamada `spawn`. `spawn` puede crear un
proceso y ejecutar en él código que tengas en un módulo cualquiera. El proceso
puede empezar en cualquier momento (asíncrono total) y se utilizan mensajes
entre procesos para sincronizarlos.

Los mensajes no tienen por qué ser `Strings`, pueden ser de cualquier tipo
(generalmente tuplas o atoms). Los mensajes se mandan con `send`, y debes usar
un `PID` (devuelto por `spawn`).

El receptor, espera mensajes con `receive`. `receive` funciona como `case`: se
pueden poner varios casos, y el primero que coincida, se ejecuta.

`receive` maneja sólo un mensaje. Si queremos recibir varios, debemos volver a
llamar al método que contiene el `receive`, de forma recursiva (y Elixir es muy
bueno con la recursividad). `receive` también acepta un parámetro, `after`,
para definir un timeout.

El autor dice que los procesos en Elixir son como los objetos en lenguajes
orientados a objectos, pero con mejor sentido del humor. El hecho es que son
muy livianos, y pueden mantener estado, así que podemos pensar en ellos como en
objetos de la programación orientada a objetos.

**Enlazar procesos**

Normalmente, un proceso no sabe cuando muere un proceso hijo. Debemos hacer
algo manualmente para que se notifique. Podemos crear procesos *enlazados*
(linked) con `spawn_link`. Por defecto, si un proceso hijo muere, mata al
proceso padre. Para controlar esto y poder escuchar el mensaje que lanza el
proceso hijo al morir, debemos *atrapar la salida* mediante
`Process.flag(:trap_exit, true)` justo antes de hacer `spawn_link`.

Dos procesos enlazados pueden comunicarse bidireccionalmente.

Elixir usa el framework OTP para construir árboles de procesos. OTP lleva mucho
tiempo en funcionamiento, y debemos confiar en que lo hace mucho mejor que
nosotros, por lo que lo usaremos prácticamente siempre. OTP incluye el concepto
de *Supervisor de procesos*. Más adelante estudiaremos temas relacionados con
OTP.

**Monitorizando procesos**

Si `spawn_link` permite comunicación bidireccional, `spawn_monitor` solo la
permite unidireccional. El proceso hijo puede notificar al padre, pero no al
revés.

```
# monitor devuelve el pid del proceso hijo y una referencia de la monitorización
res = spawn_monitor(<module>, <function>, <params>)
IO.inspect res
# => { #PID{3.3.3.3}, #Reference{1.2.3.4} }
```

También se puede monitorizar un proceso existente con `Process.monitor`.

¿Cuándo utilizar cada uno? Depende de la utilidad. Si la muerte de un hijo
debería matar al padre, usa procesos enlazados. Si la muerte/fallo de un hijo
solamente debería notificar al padre, usa monitorización.

## Aprender lo suficiente para hacer algo de utilidad

- [exercise-01-round-07.exs]: ejecutar el programa que pasa mensajes en cadena
  de un proceso a otro hasta llegar al millón de procesos.
- [exercise-02-round-07.exs]: escribir un código que cree dos procesos, y que a
  cada uno le mande un token (p.e.: "pepito" y "fulanito"), y que los procesos
lo devuelvan. En teoría, ¿es determinista el orden en el que se reciben las
respuestas? ¿Y en la práctica? En caso de que no, ¿cómo podría hacerse que
fuera determinista?.

**Resultados**

Parece que sí es determinista (al menos con dos procesos). Depende del orden en
el que se creen los procesos, incluso si invertimos el orden en el que se
envían los tokens, el primer proceso creado es el primero en responder.

- [exercise-03-round-07.exs]: usa `spawn_link` para crear un proceso, el cual
  envía un mensaje al padre y finaliza inmediatamente. Mientras, en el padre,
después de crear el proceso, espera 500ms y luego comienza a recibir todos los
mensajes que están esperando. Tracea todo lo que recibas. ¿Importa que no
estuvieras recibiendo notificaciones cuando el hijo terminó?

**Resultados**

No recibe ningún mensaje, el hijo termina, terminando al padre durante la
espera.

- [exercise-04-round-07.exs]: repite el ejercicio anterior, pero en lugar de
  terminar con `exit`, que el hijo lance una excepción. ¿qué diferencia notas?

**Resultados**

No hay mucha difrencia. El padre sigue terminando, sin escuchar ningún mensaje.
Al menos, la excepción aparece por consola, mostrándose un error diciendo que
el proceso hijo (con su PID) ha lanzado una excepción. En el ejercicio
anterior, solamente aparecía que el proceso padre terminaba, nada más.

Usando `Process.flag(:trap_exit, true)`, el proceso padre recibe mensajes:

```
$ elixir -r exercise-03-round-07.exs -e "Exercise3.run"
Parent's PID #PID<0.48.0>
PID's child #PID<0.53.0>
Received: "Hello!"
Received: {:EXIT, #PID<0.53.0>, :boom}

$ elixir -r exercise-04-round-07.exs -e "Exercise4.run"
Parent's PID #PID<0.48.0>
Child's PID #PID<0.53.0>

22:46:14.313 [error] Process #PID<0.53.0> raised an exception
** (RuntimeError) Child finished
    exercise-04-round-07.exs:19: Exercise4.child/1
Received: "Hello!"
Received: {:EXIT, #PID<0.53.0>, %{RuntimeError{message: "Child finished"},
[{Exercise4, :child, 1, [file: 'exercise-04-round-07.exs', line: 19]}]}}
```

Las diferencias están en lo recibido en el mensaje de terminación del hijo. En
caso de `exit` se recibe `:EXIT`, un PID, y la causa de la salida. En el caso
de la excepción: `:EXIT`, un PID y la excepción, parece, porque tiene pinta de
pila de llamadas, con su módulo, función, parámetros,...

- [exercise-05-round-07.exs]: repetir el ejercicio pero con `spawn_monitor`.

**Resultados**

No creo que lo esté haciendo bien. Se supone que monitorizando la comunicación
no es bidireccional, pero el padre recibe el mensaje que envía el hijo, así
como el mensaje que se envía al terminar o lanzar la excepción. La única
diferencia visible es que en lugar de recibir solamente un PID, se recibe un
PID y la referencia de monitorización.

- [exercise-06-round-07.exs]: escribir una función implementando *pararell
  map*, que es como una función `map` pero cada elemento es procesado por un
proceso distinto. Preguntas: ¿por qué es necesario guardar en la variable `me`
el PID del proceso padre? Se debe utilizar `^pid` para recibir los resultados
en orden, pero... ¿qué pasa si se utiliza `_pid`? ¿cómo hacer para que falle:
esperas, aumentar número elementos, que la función que procesa cada elemento
sea más complicada,...?

**Resultados**

Aumentando el número de elementos afecta al orden en el que se reciben los
mensajes. También he conseguido recibir mensajes en orden distinto con el
siguiente código:

```
Parallel.pmap 1..10, fn (i) ->
  # la espera es más corta según el elemento `i` se va a haciendo mayor
  wait_up_to = round(10 / i)
  :timer.sleep(wait_up_to)
  i
end
  #=> [ 7, 8, 9, 10, 5, 6, 3, 4, 2, 1 ]
```

Volviendo a poner `^pid` el orden vuelve a ser correcto.

- [exercise-07-round-07.exs]: toma como referencia un planificador (servidor de
  Fibonacci) de un ejercicio del libro y crea otro similar. Esta vez, se deben
contar las apariciones de la palabra `cat` en cada fichero que se encuentre en
un directorio dado. Cada fichero será procesado por un proceso distinto.
¿Podrías escribir el planificador de una forma más genérica?

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta
el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[comenzé]: {{ site.baseurl }}{% post_url 2016-01-17-aprendiendo-elixir %}
[modelo de actores]: https://en.wikipedia.org/wiki/Actor_model
[exercise-01-round-07.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-07/exercise-01-round-07.exs
[exercise-02-round-07.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-07/exercise-02-round-07.exs
[exercise-03-round-07.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-07/exercise-03-round-07.exs
[exercise-04-round-07.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-07/exercise-04-round-07.exs
[exercise-05-round-07.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-07/exercise-05-round-07.exs
[exercise-06-round-07.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-07/exercise-06-round-07.exs
[exercise-07-round-07.exs]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-07/exercise-07-round-07.exs

