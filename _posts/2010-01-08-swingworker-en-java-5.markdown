---
title: "SwingWorker en Java 5"
date: 2010-01-08 19:44
author: Rubén Chavarría
categories: 
- java
- swing
- swing worker
comments: true
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
  <p>Este post pertenece a mi antiguo blog en <a href="http://rchavarria.wordpress.com">wordpress</a>, pero decidí pasarme a github:pages por las siguientes <a href="/blog/2012/12/03/por-que-cambie-mi-blog-en-wordpress-com">razones</a></p>
</div>

`SwingWorker` es una clase de utilidad incluida en Java SE 6 que soluciona el problema de 
utilizar un hilo (thread) separado al de Swing para realizar tareas de larga duración. 
Anteriormente ya existían implementaciones que realizaban esta tarea, pero en la versión 
6 de Java SE se ha decidido incluirla en la propia distribución de Java. Existe un 
[backport de `SwingWorker`](https://swingworker.dev.java.net/) para utilizar 
los mismos conceptos en Java SE 5. Esta entrada es aplicable tanto para `SwingWorker` 
incluido en Java SE 6 como para el backport.

<!-- more -->

## El hilo manejador de eventos (Event Dispatching Thread)

Durante el desarrollo de interfaces gráficas suelen aparecer tareas cuya realización
conllevan mucho tiempo, por ejemplo, leer un archivo XML cuando el usuario pulse un 
botón. La forma más rápida y sencilla de realizar esta tarea podría ser los siguiente:

```java
JButton button = new JButton(&quot;Cargar fichero XML&quot;);
button.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        xmlDocument = loadXML();
    }
});
```

De esta forma, la carga del archivo se realiza en el hilo manejador de eventos 
(EDT - Event Dispatching Thread) de Swing, y como la tarea necesita mucho tiempo, 
no es posible manejar el resto de eventos que la interfaz gráfica genera y se quedara 
congelado, fijo, sin respuesta aparente, hasta que la tarea finalice. Esto produce 
un efecto indeseable de cara al usuario de la aplicación.

De hecho, a la hora de desarrollar interfaces gráficas se deberían respetar estas 
dos reglas básicas:

1. Las tareas de larga duración no deben ejecutarse nunca en el hilo manejador 
de eventos (EDT), de otra forma la aplicación no responderá al usuario
2. Los componentes gráficos se deben acceder **únicamente** desde el hilo 
manejador de eventos

Cualquier otra debería realizarse en un hilo separado (difícil pero es lo más recomendable).

## Solución

Efectivamente, la solución pasa por utilizar un hilo distinto al EDT. `SwingWorker` nos 
proporciona la base para utilizar un hilo distinto para realizar tareas costosas en 
cuanto al tiempo de ejecución. `SwingWorker` permite ejecutar tareas de larga duración 
mientras la interfaz gráfica sigue respondiendo a la interacción con el usuario.

La forma más simple de utilizar `SwingWorker` es implementando el método `doInBackground`
extendiendo la clase `SwingWorker` o creando una clase anónima:

```java
SwingWorker worker = new SwingWorker&lt;MyXMLFile, Void&gt;() {
    public MyXMLFile doInBackground() {
        MyXMLFile myXMLDoc = loadXML();
        return myXMLDoc;
    }
};
```

Para que la tarea se ejecute debemos invocar al método `execute` de `SwingWorker`. 
Dicho método se encarga de llamar a `doInBackground` asegurándose de que se 
ejecuta en un hilo diferente al EDT.

Pero, ¿cómo recupero el resultado de la larga tarea?. `SwingWorker` proporciona el método 
`get` para recuperar el resultado, pero sólo debe ser llamado una vez la tarea ha 
finalizado. Existen dos métodos para asegurarnos que la tarea ha finalizado:

1. Sobrescribiendo el método `done`, el cual es ejecutado en el hilo
manejador de eventos después de que la tarea haya finalizado.

```java
private MyXMLFile doc;
//...
SwingWorker&lt;Document, Void&gt; worker = new SwingWorker&lt;MyXMLFile, Void&gt;() {
    public MyXMLFile doInBackground() {
        MyXMLFile myXMLDoc = loadXML();
        return myXMLDoc;
    }

    public void done() {
        doc = get();
    }
};
```

2. Registrar un *listener* mediante el método 
`addPropertyChangeListener(PropertyChangeListener listener)` 
el cual será notificado de cambios en el estado de `SwingWorker`

*Actualización (26-01-2010)*: [Uso avanzado de `SwingWorker`]({{ site.baseurl }}{% post_url 2010-01-26-uso-avanzado-de-swingworker %})
