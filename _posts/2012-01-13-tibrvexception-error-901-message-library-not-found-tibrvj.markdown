---
title: "TibrvException[error=901,message=Library not found: tibrvj]"
date: 2012-01-13 13:01
author: Rubén Chavarría
categories: 
- java
- tibco
- tibrvexception
- tibrvj
comments: true
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
  <p>Este post pertenece a mi antiguo blog en <a href="http://rchavarria.wordpress.com">wordpress</a>, pero decidí pasarme a github:pages por las siguientes <a href="/blog/2012/12/03/por-que-cambie-mi-blog-en-wordpress-com">razones</a></p>
</div>

Actualmente, en el trabajo estamos utilizando TIBCO Rendezvous como 
herramienta de mensajería entre nuestras aplicaciones java, y recientemente 
me he encontrado con un problema. En este post voy a hablar de dicho problema, 
así que si no te interesa el tema, ya has terminado de leer el artículo :-)

<!-- more -->

## Problema

El problema es el siguiente: no soy capaz de que nuestras aplicaciones 
carguen la librería para poder comunicarse. Más concretamente, estoy obteniendo 
la siguiente excepción:

```
[...]
Caused by: TibrvException[error=901,message=Library not found: tibrvj]
    at com.tibco.tibrv.Tibrv.loadLib(Tibrv.java:474)
    at com.tibco.tibrv.Tibrv.open(Tibrv.java:275)
[...]
```

Antes de nada, voy a contextualizar este error:

El entorno de trabajo es un Windows 7, con procesador Inter de 64 bits, la 
versión de Tibco Rendezvous es la 8.2 y tengo instalada una JDK de java 
versión 1.6.0_17.

Googleando el error no llego a ninguna solución en concreto, sólo conversaciónes
acerca del classpath de la aplicación. Pero me he dado cuenta de que se deben 
dar unas condiciones:

- El fichero `tibrvj.jar` debe estar accesible en el classpath de 
la aplicación
- La variable de entorno `PATH` debe contener (entre otros) este 
valor: `%TIBRV_HOME%\bin`. Siendo `TIBRV_HOME` el 
directorio de instalación de Tibco Rendezvous, por ejemplo y en mi caso es: 
`"C:\tibco\tibrv\8.2"`

Cumplo todas estas condiciones, pero sigo teniendo el error.

La excepción salta cuando en mi aplicación intento cargar la librería Tibrv 
mediante el código: `Tibrv.open(Tibrv.IMPL_NATIVE);`

Como no puedo ver el código interno de la implementación de Tibco, intento 
cargar la librería al más bajo nivel, mediante: 
`System.loadLibrary("tibrvj");`

La librería debería cargar, ya que previamente he comprobado que el fichero 
`tibrvj.dll` está accesible a la aplicación, ya que ese fichero 
está localizado en el directorio `%TIBRV_HOME%\bin`, incluido en la 
variable de entorno `PATH`, y lo puedo comprobar dentro de mi 
aplicación java leyendo el valor de la variable de sistema 
`java.library.path`.

Al ejecutar el código `System.loadLibrary("tibrvj");` obtengo la 
siguiente excepción:

```
[...]
Exception in thread &quot;main&quot; java.lang.UnsatisfiedLinkError: C:\TIBCO\tibrv\8.2\bin\tibrvj.dll: Can't load AMD 64-bit .dll on a IA 32-bit platform
    at java.lang.ClassLoader$NativeLibrary.load(Native Method)
    at java.lang.ClassLoader.loadLibrary0(ClassLoader.java:1758)
    at java.lang.ClassLoader.loadLibrary(ClassLoader.java:1683)
    at java.lang.Runtime.loadLibrary0(Runtime.java:823)
    at java.lang.System.loadLibrary(System.java:1028)
[...]
```

Bueno, ya tengo una pista. Resulta que estoy intentando cargar una librería 
desarrollada para 64bits en una plataforma (java, supongo) que es de 32bits. 
Luego, voy a comprobar mi versión instalada de java y si no es de 64bits 
tendré que instalar una de 64bits.

Compruebo mi versión de java:

```
C:\&gt;java -version
java version &quot;1.6.0_17&quot;
Java(TM) SE Runtime Environment (build 1.6.0_17-b04)
Java HotSpot(TM) Client VM (build 14.3-b01, mixed mode, sharing)
```

<strong>(FAIL)</strong> No indica nada de que sea java de 64bits, por lo que 
supongo que será de 32.

## Solución

Descargo la última versión de java 1.6 de 64bits, la instalo y vuelvo a 
comprobar la versión instalada:

```
C:\&gt;java -version
java version &quot;1.6.0_29&quot;
Java(TM) SE Runtime Environment (build 1.6.0_29-b11)
Java HotSpot(TM) 64-Bit Server VM (build 20.4-b02, mixed mode)
```

Bien! ya tengo instalada una versión de java de 64bits.

Pruebo mi aplicación, ..., FUNCIONA!

## Conclusión

Todas las soluciones que encontré se centraban solamente en corregir las 
variables de entorno `PATH` y `CLASSPATH`, pero estas 
soluciones no eran suficientes para mí. Al menos, al acotar el problema mucho 
más y llegando al un nivel más bajo de abstracción obtuve una pista que me 
indicó que debería asegurarme de usar una versión de 64bits de java. Una vez 
instalada la versión correcta del JDK/JRE de java, todo funcionó.

Espero que esta información sea de utilidad a todos aquellos que tienen el
problema de encontrarse con la excepción: 
`TibrvException[error=901,message=Library not found: tibrvj]`

El código completo usado para demostrar este error se puede encontrar aquí:

```
import com.tibco.tibrv.Tibrv;
import com.tibco.tibrv.TibrvException;

public class TibrvLoaderTest {
  public static void main(String[] args) {
    new TibrvLoaderTest().start();
  }
  private void start() {
    printClasspath();
    printLibraryPath();
    testLoadLibrary();
    openTibrvjLibrary();
  }
  private void printClasspath() {
    String cp = System.getProperty(&quot;java.class.path&quot;);
    for(String cpElement : cp.split(&quot;;&quot;)){
      System.out.println(&quot;Classpath element: &quot; + cpElement);
    }
  }
  private void printLibraryPath() {
    String lp = System.getProperty(&quot;java.library.path&quot;);
    for(String lpElement : lp.split(&quot;;&quot;)){
      System.out.println(&quot;Library path element: &quot; + lpElement);
    }
  }
  private void testLoadLibrary() {
    System.loadLibrary(&quot;tibrvj&quot;);
  }
  private void openTibrvjLibrary() {
    try {
      Tibrv.open(Tibrv.IMPL_NATIVE);
    } catch (TibrvException e) {
      throw new RuntimeException(&quot;Can't load Tibrv&quot;, e);
    }
  }
}
```
