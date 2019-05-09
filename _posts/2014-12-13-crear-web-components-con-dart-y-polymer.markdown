---
title: "Crear Web Components con Dart y Polymer"
date: 2014-12-13 18:42
author: Rubén Chavarría
comments: true
categories: 
- dart
- polymer
- tutorials
published: true
footer: false
---

[Dart] es un lenguaje de programación, no muy conocido hoy en día, pero
que tiene un gran potencial, ya que está pensado para aplicaciones
web, tanto para la parte servidora como para la parte cliente. Así,
con Dart puedes escribir código que se ejecuta en el navegador y
código ejecutándose en un servidor que responda a ese cliente.

[Polymer] es una implementación del estándar HTML Web Components,
un estándar que quiere revolucionar la manera en la que se desarrollan
aplicaciones web en los navegadores.

En este tutorial describo lo que he aprendido siguiendo el tutorial acerca
de [Cómo crear un Web Component con Dart y Polymer]. Si quieres bucear
en el código directamente, puedes hacerlo en mi repositorio de Github
[Custom element Dart tutorial].

<!-- more -->

## Qué vamos a crear

El Web Component que crearemos con este tutorial es un sencillo cronómetro,
con el cual podremos comenzar a contar el tiempo, pausarlo o detenerlo completamente.

Rápidamente, los pasos que vamos a seguir son:

1. Importar el fichero HTML que contiene la definición del Web Component
2. Usar el Web Component en nuestra propia página web
3. Inicializar Polymer. La librería de Dart que vamos a usar ya proporciona
el mecanismo para hacerlo, no te preocupes

## Ficheros de los que consta el tutorial

- `web/index.html`: es el punto de entrada de la aplicación. Inicializa Polymer,
importa el Web Component y usa el mismo.
- `web/tute_stopwatch.html`: código HTML que define el Web Component.
importa el Web Component y usa el mismo.
- `web/tute_stopwatch.dart`: código Dart que implementa el Web Component.

## Instalando Polymer.dart

Para poder usar Polymer, primero es necesario instalarlo como una dependencia del
proyecto. Para ello, modificar el fichero `pubspec.yaml` y añadir el siguiente
contenido: 

``` 
dependencies:
  polymer: ">=0.15.1 <0.16.0"
``` 

Después, ejecutar el comando `pub get`. `pub` es una herramienta que viene con el
SDK de Dart. Dart Editor también puede ejecutar este comando para instalar todas
las dependencias del proyecto.

Para inicializar Polymer, modificar `web/index.html` y añadir esta línea al final
del mismo:

``` html
...
<script type="application/dart">export "package:polymer/init.dart";</script>
...
```

## Incluir Polymer en la aplicación

Estos son los ficheros a modificar para usar Polymer en la creación del
Web Component:

`web/tute_stopwatch.html`: importar el fichero `packages/polymer/polymer.html`
antes de definir cualquier Web Component en la aplicación:

``` html
<link rel="import" href="packages/polymer/polymer.html">
<polymer-element name="tute-stopwatch">
```

`web/tute_stopwatch.dart`: importar la librería Polymer en el fichero Dart:

``` 
import 'dart:html';
import 'package:polymer/polymer.dart';
// ...
```

## Instanciar un Web Component

En la página web donde se va a usar el Web Component, debemos importar la definición
del mismo, usar un tag con su nombre (como si fuera un componente HTML normal) e
inicializar Polymer. De forma que `web/index.html` quedaría parecido a:

``` html
<!DOCTYPE html>
<html>
  <head>
    <!-- importa la definición del Web Component -->
    <link rel="import" href="tute_stopwatch.html">
  </head>
 
  <body>
    <!-- usa el Web Component -->
    <tute-stopwatch></tute-stopwatch>
    
    <!-- inicializa Polymer -->
    <script type="application/dart">export "package:polymer/init.dart";</script>
  </body>
</html>
```

## Definiendo el Web Component

La definición del mismo está en el fichero `web/tute_stopwatch.html`. Para definirlo
hay que usar el tag `<polymer-element>` y asignar un nombre al Web Component. En
este caso `tute-stopwatch`.

El tag `<polymer-element>` puede tener dos tags hijos: `<template>`, que contiene
el código HTML; y `<script>`, que contiene el código Dart.

``` html
<polymer-element name="tute-stopwatch">
  <template>
    ...
  </template>
  <script type="application/dart" src="tute_stopwatch.dart"></script>
</polymer-element>
```

## Dando comportamiento al Web Component

El comportamiento es implementado en Dart, en el fichero `web/tute_stopwatch.dart`.
En este fichero, se declara una clase que extiende de `PolymerElement` y está 
anotada con `@CustomTag`. El contenido de `@CustomTag` debe coincidir con el
nombre dado en la definición del Web Component.

```
@CustomTag('tute-stopwatch')
class TuteStopwatch extends PolymerElement {
    TuteStopwatch.created() : super.created();
}
```

Para que todo esté correcto, la clase `TuteStopwatch` debe heredar de `PolymerElement` o
implementar las interfaces `Polymer` y `Observable`. Además, debe definir un
constructor *nombrado* que llame a `super.created()`.

## Enlazando datos entre Dart y HTML

En la parte visual (HTML) se pueden usar las llaves dobles `{% raw %}{{...}}{% endraw %}` para utilizar una
variable anotada como `@observable` en la parte de comportamiento (Dart). Por ejemplo,
para usar una `String` que al modificarla en Dart se actualice la vista HTML, los
ficheros `web/tute_stopwatch.html` y `web/tute_stopwatch.dart` quedarían:

``` html
<polymer-element name="tute-stopwatch">
  <template>
    <div>{% raw %}{{counter}}{% endraw %}</div>
  </template>
  ...
</polymer-element>
```

``` 
@CustomTag('tute-stopwatch')
class TuteStopwatch extends PolymerElement {
    ...
    @observable String counter;

    void aMethod() {
        counter = '14:59';
    }
}
```

Para hacer un doble enlace, de Dart a HTML y viceversa, se puede consultar en enlace
[Two-way data binding using Polymer].

## Creando manejadores de eventos

De la misma forma que se puede enlazar variables, se pueden enlazar manejadores de
eventos que gestionen las interacciones del usuario. Por ejemplo, para responder
ante un click del usuario, en HTML:

``` html
<button on-click="{% raw %}{{start}}{% endraw %}">Start</button>
```

Mientras que en Dart:

``` 
@CustomTag('tute-stopwatch')
class TuteStopwatch extends PolymerElement {
    ...
    void start(Event evt, var detail, Node target) {
        ...
    }
}
```

Donde:

- `evt`: contiene información sobre el evento
- `detail`: puede proveer información adicional sobre el evento
- `target`: el nodo HTML que lanzó el evento

Para más información, como los manejadores de eventos disponibles y más, consultar
[Declarative event mapping].

## Desplegando la aplicación

Antes de desplegar, es necesario el uso de *transformadores* de Polymer para
completar el proceso. Para ello, modificar `pubspec.yaml` añadiendo las siguientes
líneas:

```
...
dependencies:
  polymer: ...
transformers:
- polymer:
    entry_points: web/index.html
```

Definiendo `entry_points` indicamos a Polymer qué ficheros HTML queremos que transforme.

Para probar el Web Component desarrollado podemos seleccionar *Ejecutar como JavaScript*
sobre el fichero `web/index.html` desde Dart Editor.

O también, tenemos el comando `pub serve` en línea de comandos. Este comando nos indicará
una dirección URL donde poder probar la aplicación.

El comando `pub build` genera ficheros que pueden ser desplegados en un servidor
aparte y que hará posible ejecutar la aplicación en cualquier navegador moderno.

[Dart]: http://dartlang.org
[Polymer]: http://polymer-project.org
[Custom element Dart tutorial]: https://github.com/rchavarria/dart-tutorials/tree/master/custom-element-dart-tutorial
[Cómo crear un Web Component con Dart y Polymer]: https://www.dartlang.org/docs/tutorials/polymer-intro/
[Two-way data binding using Polymer]: https://www.dartlang.org/docs/tutorials/forms/#binding-data
[Declarative event mapping]: http://www.polymer-project.org/polymer.html#declarative-event-mapping
