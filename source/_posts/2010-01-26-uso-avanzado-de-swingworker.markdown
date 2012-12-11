
---
layout: page
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

En una entrada anterior vimos cómo hacer un <a href="/blog/2010/01/08/swingworker-en-java-5/">uso básico de SwingWorker</a> así como cuándo usarlo. Vimos que había dos métodos de recuperar el resultado de nuestros cálculos o tarea de larga duración.

Aquí veremos un uso avanzado de <code>SwingWorker</code>. Para ello realizaremos una sencilla aplicación que calcule los <strong>N</strong> primeros números de la serie de fibonacci, los vaya mostrando en un área de texto según los vaya calculando y mostraremos el progreso de la tarea un una barra de progreso.

<!-- more -->

La clase <code>SwingWorker</code> tiene la siguiente definición: <code>SwingWorker&lt;T, V&gt;</code>. En la entrada anterior vimos que la forma básica de recuperar el resultado de nuestros cálculos era a través del método <code>get()</code>, el cuál retorna un valor de tipo genérico <strong>T</strong>. El genérico <strong>V</strong> es el tipo de datos que admiten los métodos <code>publish</code> y <code>process</code> y es el tipo de datos en el que generaremos los resultados intermedios.

Para realizar nuestra tarea del cálculo de los números de fibonacci crearemos una clase <code>FibonacciWorker</code> que herede de <code>SwingWorker</code> y que haga uso de los métodos adecuados para notificar el progreso hecho en los cálculos. Esta notificación la haremos a través de eventos de cambios en una propiedad. Es posible utilizar <code>PropertyChangelListeners</code> con propiedades definidas por nosotros y utilizar el método <code>firePropertyChange</code> para lanzar estos eventos. Para este ejemplo utilizaremos la propiedad <code>progress</code> que es una propiedad que ya está enlazada por defecto. La propiedad <code>state</code> (indica el estado de la ejecución de la tarea: <em>INCIADA</em>, <em>CANCELADA</em>, <em>COMPLETADA</em>, ...) también lo está.

{% codeblock Nuestra tarea hereda de SwingWorker %}
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
{% endcodeblock %}

En el código anterior se han omitido detalles de implementación para no desviar la atención. Del código anterior cabe destacar la llamada a <code>publish</code> en la línea <strong>11</strong>, la llamada a <code>setProgress</code> (línea <strong>12</strong>) y la implementación del método <code>process</code>.

Mediante la llamada al método <code>publish</code> indicamos a <code>SwingWorker</code> que vaya almacenando resultados intermedios con los cuales llamará al método <code>process</code>, el cual hemos sobrescrito y lo usaremos para mostrar esos resultados intermedios. Es muy importante recalcar que mientras el método <code>publish</code> se ejecuta en el hilo (thread) del cálculo exhaustivo, el método <code>process</code> se invoca en el <strong>Event Dispatching Thread (EDT)</strong>, y es por ello por lo que es seguro actualizar el interfaz de usuario.

Con la llamada al método <code>setProgress()</code> estamos indicando que se lance un evento de cambio sobre la propiedad <code>progress</code> (propiedad creada por defecto junto con <code>state</code> para la notificación de cambios en propiedades). El evento propagado incluirá entre sus datos el parámetro que recibe la función. Para mostrar ese progreso utilizaremos una barra de progreso, la cual la registraremos como interesada en recibir eventos de cambios en las propiedades de <code>FibonacciWorker</code>.

{% codeblock Actualizar una barra de progreso %}
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
{% endcodeblock %}

En el siguiente enlace es posible ver una aplicación demostrando lo aprendido. Si se desea descargar el código fuente en forma de proyecto de NetBeans: <a href="http://kenai.com/projects/rchavarria/downloads/download/fibonacci%252FFibonacciCalculator%2520NB%2520project.zip"><strong>FibonacciWorker NetBeans project</strong></a>.

<a href="http://kenai.com/projects/rchavarria/downloads/download/fibonacci%252Flaunch.jnlp"><img class="center" title="Ejecutar FibonacciCalculator" src="/images/wordpress/launch.png" alt="" width="88" height="23" /></a>
<div id="_mcePaste" style="overflow:hidden;position:absolute;left:-10000px;top:285px;width:1px;height:1px;">http://rchavarria.wordpress.com/2010/01/08/swingworker-en-java-5/</div>
