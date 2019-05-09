---
title: "Elixir: octavo asalto"
date: 2016-12-31 19:13
author: Ruben Chavarria
comments: true
categories: 
- learning
- elixir
published: true
footer: false
sidebar: true
---

Último post del año, que no de la serie sobre aprender [Elixir]. Este asalto va de nodos, PIDs y un poquito (muy poco) de entrada/salida.

Aprenderemos qué es un nodo, cómo crear nuevos nodos y cómo comunicarlos a un nivel muy básico. Y algo muy interesante, cómo hacer que un nodo ejecute una función a nuestro antojo.

Todo esto, siguiendo el [método de aprendizaje] con el que comenzé la serie:

- Aprender lo suficiente para comenzar
- Experimentar, jugar, buscar puntos desconocidos, hacerse preguntas
- Aprender lo suficiente para hacer algo de utilidad
- Enseñar lo aprendido

![Eighth]({{ site.baseurl }}/assets/images/2016/risk.jpg)

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen basada en <a href="https://flic.kr/p/3pUVs">Risk</a> de <a href="https://www.flickr.com/photos/benstephenson/">Ben Stephenson</a>, <a href="https://creativecommons.org/licenses/by/2.0/">algunos derechos reservados</a>, licencia: <a href="https://creativecommons.org/licenses/by/2.0/">CC BY 2.0</a>
  </span>
</div>

<!-- more -->

## Aprender lo suficiente para comenzar

#### Nodos - La clave para los servicios distribuidos

Un **nodo** no es más que una instancia de la máquina virtual de Erlang
ejecutándose. Es como un sistema operativo completo, y ofrece servicios como
tal a procesos locales o remotos.

##### Nombres de nodos

En `iex`, podemos saber el nombre del nodo actual con `Node.self`:

```
iex> Node.self
:"rchavarria@localhost"
```

Podemos dar un nombre al nodo al iniciar `iex`:

```
$ iex -name foobar@localhost
iex(foobar@localhost)> Node.self
:"foobar@localhost"
```

Si te fijas, el valor devuelto por `Node.self` tiene los dos puntos delante,
como si fuera un `Atom`. Y es que en Elixir, los nombres de los nodos son
tratados como `Atom`s, lo que hace super sencillo referenciar nodos en el
código.

También, podemos saber qué nodos conoce un nodo al que estemos conectados:

```
iex(node_two)> Node.list
[]

# y al conectarnos a un nodo, aparecerá como conectado
iex(node_two)> Node.connect :"node_one@localhost"
true
iex(node_two)> Node.list
[ :"node_one@localhost" ]
```

Podemos ejecutar una función en un nodo remoto:

```
iex(node_one)> func = fn -> IO.puts "Hello, I'm in #{inspect Node.self}"
iex(node_one)> Node.spawn( :"node_two@localhost", func )
Hello, I'm in :"node_two@localhost"
```

`Node.spawn` es impresionante. Podemos ejecutar una función en otro nodo
fácilmente. Pero aunque se ejecute en `node_two`, hereda lo que se llama *group
leader*, con lo que es capaz de mostrar mensajes por consola en `node_one` (en
lugar del dos, que es donde se ejecuta).

Además de poder dar un nombre a un nodo, podemos establecer su *cookie*. La
cookie de un node no es más que un token, y se utiliza para permitir que los
nodos se conecten entre sí. Nodos con la misma cookie se pueden conectar. Si es
distinta, los nodos rechazarán la conexión. Las cookies se mandan en texto
plano, así que cuidado con las conexiones a través de internet.

##### Nombrando tus procesos

Cada proceso se identifica con un PID. Un PID está compuesto por tres números,
aunque sólo contiene dos campos: el número de nodo (`0` si el nodo es el local)
y el número de proceso en sí. Este número de proceso está compuesto por sus
bits más y menos representativos (de ahí que veamos tres números en un PID como
éste `#PID<0.71.0>`). El id de node es el id del nodo donde *vive* el proceso.

#### Entrada/salida, PIDs y Nodos

La entrada/salida en la máquina virtual de Erlang se hace a través de
servidores de entrada/salida. Elixir y Erlang proporcionan librerías para no
tener que lidiar con ellos, ya que son a muy bajo nivel.

En Elixir, se identifica un fichero por el PID del proceso del servidor de
entrada/salida que lo está manejando.

Por ejemplo, la función `IO.puts` utiliza el PID devuelto por
`:erlang.group_leader()` como valor por defecto para enviar una cadena al
proceso que la muestra por consola: `send :erlang.group_leader(), str` podría
ser el código equivalente.

## Aprender lo suficiente para hacer algo de utilidad

- Ejercicio 1: en el código del servidor de ticks ([ticker.ex]), el autor habla
de que el tick se envía cada 2 segundos más o menos.  Pero el timeout está
puesto a 2 segundos exactos. ¿Por qué habla de *más o menos*?

**Respuesta**

El timeout es de justo 2 segundos, pero el timeout solo saltará si no se
registra ningún cliente en esos 2 segundos. Si un cliente se registra (digamos
en el momento 1.55 segundos) no saltará el timeout hasta los 3.55 segundos
siguientes (1.55 segundos que pasaron desde el anterior tick hasta el registro
del último cliente más 2 segundos del timeout normal).

- Ejercicio 2: modificar el servidor de ticks para que mande solo un
tick cada vez, de forma circular, a cada uno de los clientes registrados (el
primer tick al primer cliente, el segundo tick al segundo cliente
registrado,...). El programa deberá lidiar con nuevos clientes registrados.

- Ejercicio 3: reimplementar el servidor de ticks, pero esta vez
debe ser circular, de forma que el cliente 1 mande un tick al cliente 2.
Pasados 2 segundos, el cliente 2 mandará un tick al 3. Y así hasta el último, el cual
enviará un tick al 1. Y vuelta a empezar. El problema está en cómo añadir
clientes al círculo (o *ring*) y quién tiene la responsabilidad de actualizar
ese círculo de clientes.

**Respuesta**

Me costó un tiempo dar con la solución al ejercicio ([ring_ticker.ex]). Puede
que el *ring* lo tenga que gestionar el servidor central. De otra forma, los
clientes perderán el timeout del `receive` y se volverán un poco locos. 

## Enseñar lo aprendido, y repetir desde el paso 7

Aquí está, este post, mis notas, mis pensamientos, mis dudas y mi código. Hasta
el siguiente asalto.

[Elixir]: http://elixir-lang.org/
[método de aprendizaje]: {{ site.baseurl }}{% post_url 2016-01-17-aprendiendo-elixir %}
[ticker.ex]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-08/ticker.ex
[ring_ticker.ex]: https://github.com/rchavarria/learning-elixir/blob/master/code/round-08/ring_ticker.ex

