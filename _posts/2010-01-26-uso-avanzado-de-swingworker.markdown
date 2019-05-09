---
title: "Uso avanzado de SwingWorker"
date: 2010-01-26 09:44
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

En una entrada anterior vimos cómo hacer un 
[uso básico de `SwingWorker`]({{ site.baseurl }}{% post_url 2010-01-08-swingworker-en-java-5 %})
así como cuándo usarlo. Vimos que había dos métodos de recuperar el resultado de nuestros 
cálculos o tarea de larga duración.

Aquí veremos un uso avanzado de `SwingWorker`. Para ello realizaremos una sencilla aplicación 
que calcule los `N` primeros números de la serie de Fibonacci, los vaya mostrando en un 
área de texto según los vaya calculando y mostraremos el progreso de la tarea un una barra 
de progreso.

<!-- more -->

La clase `SwingWorker` tiene la siguiente definición: `SwingWorker<T, V>`. En la entrada 
anterior vimos que la forma básica de recuperar el resultado de nuestros cálculos era a 
través del método `get()`, el cuál retorna un valor de tipo genérico `T`. El genérico 
`V` es el tipo de datos que admiten los métodos `publish` y `process` y es el tipo de datos 
en el que generaremos los resultados intermedios.

Para realizar nuestra tarea del cálculo de los números de Fibonacci crearemos una clase 
`FibonacciWorker` que herede de `SwingWorker` y que haga uso de los métodos adecuados 
para notificar el progreso hecho en los cálculos. Esta notificación la haremos a través 
de eventos de cambios en una propiedad. Es posible utilizar `PropertyChangelListeners` con 
propiedades definidas por nosotros y utilizar el método `firePropertyChange` para lanzar 
estos eventos. Para este ejemplo utilizaremos la propiedad `progress` que es una propiedad 
que ya está enlazada por defecto. La propiedad `state` (indica el estado de la ejecución 
de la tarea: `INCIADA`, `CANCELADA`, `COMPLETADA`, ...) también lo está.

```java
class FibonacciWorker extends SwingWorker&lt;List&lt;Integer&gt;, Integer&gt; {
  PrimeNumbersTask(JTextArea textArea, int numbersToCalculate) {
    //initialize
  }

  @Override
  public List&lt;Integer&gt; doInBackground() {
    while (numbers.size &lt;= numberstoCalculate &amp;&amp; !isCancelled()) {
      number = nextFibonacciNumber();
      numbers.add(number);
      publish(number);
      setProgress(100 * numbers.size() / numbersToCalculate);
    }
    return numbers;
  }

  @Override
  protected void process(List&lt;Integer&gt; chunks) {
    for (Integer number : chunks) {
      textArea.append(number + &quot;\n&quot;);
    }
  }

  private Integer nextFibonacciNumber(){
    //  calculate next fibonacci number and return it
  }
}
```

En el código anterior se han omitido detalles de implementación para no desviar la 
atención. Del código anterior cabe destacar la llamada a `publish` en la línea 11, 
la llamada a `setProgress` (línea 12) y la implementación del método `process`.

Mediante la llamada al método `publish` indicamos a `SwingWorker` que vaya almacenando 
resultados intermedios con los cuales llamará al método `process`, el cual hemos 
sobrescrito y lo usaremos para mostrar esos resultados intermedios. Es muy importante 
recalcar que mientras el método `publish` se ejecuta en el hilo (thread) del cálculo 
exhaustivo, el método `process` se invoca en el *Event Dispatching Thread (EDT)*, y 
es por ello por lo que es seguro actualizar el interfaz de usuario.

Con la llamada al método `setProgress()` estamos indicando que se lance un evento de 
cambio sobre la propiedad `progress` (propiedad creada por defecto junto con `state` 
para la notificación de cambios en propiedades). El evento propagado incluirá entre 
sus datos el parámetro que recibe la función. Para mostrar ese progreso utilizaremos 
una barra de progreso, la cual la registraremos como interesada en recibir eventos de 
cambios en las propiedades de `FibonacciWorker`.

```java
final JProgressBar progressBar = new JProgressBar(0, 100);
FibonacciWorker task = new FibonacciWorker(textArea, numbersToCalculate);
task.addPropertyChangeListener(
  new PropertyChangeListener() {
    public  void propertyChange(PropertyChangeEvent evt) {
      if ("progress".equals(evt.getPropertyName())) {
        progressBar.setValue((Integer)evt.getNewValue());
      }
    }
  });
```

En el siguiente enlace es posible ver una aplicación demostrando lo aprendido. Si se 
desea descargar el código fuente en forma de proyecto de NetBeans: 
[FibonacciWorker NetBeans project](http://kenai.com/projects/rchavarria/downloads/download/fibonacci%252FFibonacciCalculator%2520NB%2520project.zip)

[![Ejecutar FibonacciCalculator]({{ site.baseurl }}/assets/images/wordpress/launch.png)](http://kenai.com/projects/rchavarria/downloads/download/fibonacci%252Flaunch.jnlp)

### Posts relacionados

- [Uso básico de `SwingWorker`]({{ site.baseurl }}{% post_url 2010-01-08-swingworker-en-java-5 %})
