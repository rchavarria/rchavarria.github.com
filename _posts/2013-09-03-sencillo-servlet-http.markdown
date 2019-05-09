---
title: "Un sencillo servlet HTTP"
date: 2013-09-03 13:41
comments: true
categories: 
categories: 
- tutorials
- Java EE
- programming
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
    Find a lightweight English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/simple-http-servlet">source code repository</a>.
</div>

En este post veremos cómo crear un sencillo servlet HTTP. La configuración de dicho
servlet la haremos mediante anotaciones, y así veremos cómo Java EE 6 puede
ahorrarnos a los desarrolladores cierto trabajo con ficheros XML de configuración.

Se puede ver el código fuente de la demostración en el directorio 
[`simple-http-servlet`](https://github.com/rchavarria/javaee-6-demos/tree/master/simple-http-servlet)
del repositorio de las demos en github.

<!-- more -->

## Demo

La demostración va a ser muy sencilla: crearemos en servlet, lo configuraremos
para que responda cuando un usuario visite una página web en concreto, y haremos
que responda de una forma muy, pero que muy sencilla.

Para ejecutar la demo, simplemente hay que descargase el código fuente y ejecutar
`mvn jetty:run` desde el directorio raiz de la demo. Ya se puede ver el resultado
del servlet visitando 
[http://localhost:8080/SimpleHttpServlet](http://localhost:8080/SimpleHttpServlet).

![Respuesta del servlet]({{ site.baseurl }}/assets/images/2013/simple-http-servlet.png)

## Dependencias

Para esta demostración usaremos [Apache Maven](http://maven.apache.org/) para 
la gestión de dependencias. Esto nos facilitará enormemente nuestra labor de
programación. Si echamos un vistazo al fichero `pom.xml` de la demo, podremos
ver que solamente existe una dependencia externa, `javax-servlet-api`, que es
la que nos permitirá crear nuestro servlet.

## El servlet

Como ya he comentado antes, se trata de un servlet HTTP, luego nuestro servlet
heredará de `javax.servlet.http.HttpServlet`. 

Java EE 6 nos permite configurar los servlets sin hacer uso del fichero descriptor
de la aplicación web, `web.xml`. Esto es posible mediante la anotación `@WebServlet`.
Suponiendo que queremos que el servlet responda cuando el usuario visite la dirección
`/SimpleHttpServlet`, la signatura de la clase de nuestro servlet quedaría:

``` java
@WebServlet(urlPatterns = {"/SimpleHttpServlet"})
public class HttpServletDemo extends HttpServlet {
    //...
}
```
### Respuesta del servlet

El objetivo de la demo es ver cómo configurar un servlet HTTP mediante anotaciones,
por lo que la respuesta proporcionada por él es lo más sencilla posible: obtiene
un `writer` de la respuesta HTTP y escribe un sencillo mensaje en texto plano.

``` java
PrintWriter out = response.getWriter();
try{
    out.println("<h2>");
    out.println("This servlet has been configured simply by: ");
    out.println("@WebServlet(urlPatterns = {\"/SimpleHttpServlet\"})");
    out.println("</h2>");
} finally {
    out.close();
}
```

Para echar un ojo al código fuente, visitar el directorio 
[`simple-http-servlet`](https://github.com/rchavarria/javaee-6-demos/tree/master/simple-http-servlet).
