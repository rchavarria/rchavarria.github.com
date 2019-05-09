---
title: "Leer parámetros desde un servlet"
date: 2013-09-13 12:39
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
    Find a lightweight English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/request-parameters">source code repository</a>.
</div>

En este post veremos cómo un servlet puede leer los parámetros que vienen 
encapsulados en la petición HTTP que realiza un usuario a nuestra aplicación web.
La configuración de dicho servlet la haremos mediante anotaciones para tener un
proyecto más sencillo.

Se puede ver el código fuente de la demostración en el directorio 
[`request-parameters`](https://github.com/rchavarria/javaee-6-demos/tree/master/request-parameters)
del repositorio de las demos en github.

<!-- more -->

## Demo

La demostración va a ser muy sencilla: crearemos en servlet, lo configuraremos
para que responda cuando un usuario envíe los campos de un formulario de login,
y haremos que responda con una página HTML que incluye una lista con los valores
de los campos de dicho formulario.

Para ejecutar la demo, simplemente hay que descargase el código fuente y ejecutar
`mvn jetty:run` desde el directorio raiz de la demo. Visitar la página de login
[http://localhost:8080/login.html](http://localhost:8080/login.html), introducir
unos valores cualquiera y enviar los datos del formulario. Veremos el resultado
que devuelve el servlet al leer los parámetros de la petición HTTP que hemos
enviado al servidor.

![Respuesta del servlet]({{ site.baseurl }}/assets/images/2013/request-parameters.png)

## Dependencias

Para esta demostración usaremos [Apache Maven](http://maven.apache.org/) para 
la gestión de dependencias. Esto nos facilitará enormemente nuestra labor de
programación. Si echamos un vistazo al fichero `pom.xml` de la demo, podremos
ver que solamente existe una dependencia externa, `javax-servlet-api`, que es
la que nos permitirá crear nuestro servlet.

## Página de login

![Respuesta del servlet]({{ site.baseurl }}/assets/images/2013/login-form.png)

La entrada a nuestra demo será la página de login, la cual contiene un formulario
muy simple, con dos campos principales: email del usuario y contraseña. 

En el código HTML de la página, se ha establecido la acción del formulario a
`RequestParametersServlet`. Ésta va a ser la URL a la que nuestro servlet deberá responder.

``` html
<form action="RequestParametersServlet">
	<input type="text" name="email" placeholder="Email address" autofocus />
	<input type="password" name="password" placeholder="Password" />
	
	<button type="submit">Log me in</button>
</form>
```

## El servlet

Nuestro servlet se trata de un servlet HTTP, luego heredará de `javax.servlet.http.HttpServlet`.
Lo configuraremos mediante anotaciones, con `@WebServlet`. Y retornará un sencillo 
código HTML que mostrará al usuario el valor de los parámetros enviados desde el 
formulario de login.

La definión del servlet quedaría así: 

``` java
@WebServlet(urlPatterns = {"/RequestParametersServlet"})
public class RequestParametersServletDemo extends HttpServlet {
    //...
}
```

Mientras que el código que lee los parámetros de la petición HTTP estaría agrupado en un 
método con esta pinta: 

``` java
private String outputParametersList(HttpServletRequest request) {
    Enumeration<String> names = request.getParameterNames();
	if(!names.hasMoreElements()) return "";
	
	StringBuilder sb = new StringBuilder();
	
	sb.append("<ul>");
    while(names.hasMoreElements()) {
    	String name = names.nextElement();
    	String value = request.getParameter(name);
    	
    	sb.append("<li>");
        sb.append(name + ": " + value);
        sb.append("</li>");
    }
    sb.append("</ul>");
	
	return sb.toString();
}
```

Para echar un ojo al código fuente, visitar el directorio 
[`request-parameters`](https://github.com/rchavarria/javaee-6-demos/tree/master/request-parameters).

## Enlaces relacionados

- [The open tutorials](http://theopentutorials.com/examples/java-ee/servlet/get-all-parameters-in-html-form-using-getparameternames): cómo leer todos los campos de un formulario en un servlet.
- [Leer un parámetro en un servlet](https://baurdotnet.wordpress.com/2011/01/31/getting-a-request-parameter-in-a-servlet)
