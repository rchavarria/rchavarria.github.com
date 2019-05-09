---
title: "Servlet redirecciona a una JSP"
date: 2013-09-17 13:27
comments: true
categories: 
- tutorials
- Java EE
- programming
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
    Find a lightweight English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/request-parameters-jsp">source code repository</a>.
</div>

Este post es una pequeña extensión del anterior, un servlet que leía los parámetros
de una petición HTTP. La demo anterior presentaba los parámetros leídos de una
forma muy tosca y básica. En esta demo, la información se va a presentar al usuario
de una forma más trabajada. Además, orientándonos hacia una arquitectura MVC, 
separaremos las tareas de lectura de los parámetros y presentación de los datos.

Se puede ver el código fuente de la demostración en el directorio 
[`request-parameters-jsp`](https://github.com/rchavarria/javaee-6-demos/tree/master/request-parameters-jsp)
del repositorio de las demos en github.

<!-- more -->

## Demo

La demostración va a ser muy sencilla: crearemos en servlet, lo configuraremos
para que responda cuando un usuario envíe los campos de un formulario de login,
y haremos que redireccione a una página JSP, esta página se encargará de renderizar
los datos que viajarán como atributos de la petición.

Para ejecutar la demo, simplemente hay que descargase el código fuente y ejecutar
`mvn jetty:run` desde el directorio raiz de la demo. Visitar la página de login
[http://localhost:8080/login.html](http://localhost:8080/login.html), introducir
unos valores cualquiera y enviar los datos del formulario. Como resultado, veremos
el renderizado de la página JSP en el navegador.

![Respuesta del servlet]({{ site.baseurl }}/assets/images/2013/request-parameters-jsp.png)

## Dependencias

Como viene siendo habitual, para la demostración usaremos
[Apache Maven](http://maven.apache.org/) para la gestión de dependencias. 
En nuestro fichero `pom.xml` incluiremos la única dependencia del proyecto,
`javax-servlet-api` y listo.

## El servlet

Nuestro servlet se trata de un servlet HTTP, luego heredará de `javax.servlet.http.HttpServlet`.
Lo configuraremos mediante anotaciones, con `@WebServlet`. Primero leerá los parámetros
enviados en la petición HTTP, igual que vimos en la anterior demo, y lo almacenará como un
atributo del objeto `request`, para que pueda ser leído por nuestra página JSP.

```java
//...
List<Parameter> params = buildParamList(request);
request.setAttribute("params", params);
//...
```

Luego, redireccionará la petición a nuestra página JSP. Se ha decidido hacer un 
`forward` de la petición en lugar de hacer una redirección completa, 
ya que la redirección provocaría una nueva petición HTTP y perderíamos los parámetros
de la petición original, y esto es algo que no deseamos.

```java
//...
request.getRequestDispatcher("/params.jsp").forward(request, response);
//...
```

## La página JSP 

Finalmente, la página JSP se encarga de presentar la información. De esta forma tenemos
construida nuestra demo siguiendo un patrón MVC (aunque es muy sencillo en este caso, ya 
que solo contamos con un servlet y una página JSP), donde la página JSP juega el papel
de _vista_. 

El código que nos interesa dentro del JSP es el que se encarga de iterar el 
atributo que estableció el servlet, al que hemos llamado `params`.

```html
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<ul>
	<c:forEach var="p" items="${params}">
		<li>${p.key}: ${p.value}</li>
	</c:forEach>
</ul>
``` 

## Código fuente

Para echar un ojo al código fuente, visitar el directorio 
[`request-parameters-jsp`](https://github.com/rchavarria/javaee-6-demos/tree/master/request-parameters-jsp).
