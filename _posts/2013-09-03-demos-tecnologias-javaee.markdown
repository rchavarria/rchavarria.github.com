---
title: "Demos de tecnologías Java EE"
date: 2013-09-03 12:55
comments: true
categories: 
- tutorials
- Java EE
- programming
published: true
footer: false
sidebar: true
---

Este post va a servir de índice o tabla de contenidos para una serie de post que
me gustaría ir escribiendo poco a poco, sin prisa pero sin pausa, que el blog ya
lleva mucho tiempo si actualizarse y hay que darle vida.

Estos posts van a tratar sobre tecnologías Java EE, de cómo usar estas tecnologías
en nuestros proyectos software y de cómo estas tecnologías nos permiten crear 
aplicaciones. Intentaré que estas aplicaciones estén más orientadas a las aplicaciones
web.

Comenzaré con temas y aplicaciones muy sencillas, que prácticamente no tienen sentido
en el Mundo Real™, pero que me permitirán ir adentrándome en todo el mundo Java EE.

<!-- more -->

Lista de posts:

- [Un sencillo servlet HTTP]({{ site.baseurl }}{% post_url 2013-09-03-sencillo-servlet-http %}): En este post veremos 
que crear un servlet en Java EE 6 es sincillísimo, y que incluso no es necesario
contar con un archivo descriptor de la aplicación web.
- [Acceder a los datos de un formulario desde un servlet]({{ site.baseurl }}{% post_url 2013-09-13-servlet-lee-parametros %}):
Es posible acceder a datos enviados por el usuario en la petición HTTP desde un servlet. 
En este post veremos cómo.  
- [Cómo redireccionar de un servlet a un JSP]({{ site.baseurl }}{% post_url 2013-09-17-servlet-redirecciona-jsp %}):
En esta ocasión vamos un paso más allá en los servlets, y avanzamos hacia 
una arquitectura MVC, separando la lógica de la aplicación (leer parámetros) de la
presentación, que en este caso la hará una página JSP.
- [Cómo crear un servicio web]({{ site.baseurl }}{% post_url 2013-09-19-crear-servicio-web-jaxws %}): 
En esta demo veremos cómo crear un servicio web, y de cómo usar el framework Apache CXF
para su creación, configuración y despliegue en un contenedor web. Crearemos un servicio
web basado en la especificación JAX-WS, que intercambiará mensajes SOAP sobre HTTP.
- [Cómo crear un cliente de servicio web]({{ site.baseurl }}{% post_url 2013-09-26-crear-cliente-servicio-web %}):
Aquí veremos cómo crear un sencillo cliente que consuma el servicio web creado en la demo
anterior. Lo haremos mediante un test de JUnit, y así crearemos nuestro primer test
de integración.
- [Entendiendo el ciclo de vida de entidades JPA]({{ site.baseurl }}{% post_url 2013-09-29-entendiendo-ciclo-vida-entidades-jpa %}):
Aquí aprenderemos qué estados son posibles para una entidad JPA, qué significan 
y cómo transicionar de unos a otros.
- [Apache MyFaces como implementacion de JavaServer Faces]({{ site.baseurl }}{% post_url 2013-10-28-myfaces-implementacion-javaserver-faces %}):
En esta demo crearemos desde cero una applicación web con el framework MVC MyFaces, 
la implementación de Apache de JavaServer Faces.
- [Aplicación web RESTful con Spring MVC]({{ site.baseurl }}{% post_url 2014-01-22-restful-spring-mvc %}): En esta ocasión
crearemos una aplicación web, con apariencia de aplicación REST, y para ello usaremos la
tecnología Spring MVC.
- Servlet listeners: Veremos el uso que le podemos dar a los distintos listeners asociados
a los servlets y su ciclo de vida: ServletContextListener, 
ServletContextAttributeListener, ServletRequestListener y HttpSessionListener.
- Crear una EJB sin estado: Aquí crearemos una EJB local sin estado y accederemos a
ella a través de un servlet, que será quien responda al usuario de nuestra aplicación.
- Crear una EJB remota: En esta ocasión crearemos una EJB sin estado y remota, de forma
que se pueda acceder a ella desde una aplicación cliente, que también la desarrollaremos.

Más adelante ya iré viendo por dónde seguirían las demos: páginas JSPs,
filtros para los servlets, logging, datos en la sesión, redirección...

<!-- 
	Por donde seguir?

	http://www3.ntu.edu.sg/home/ehchua/programming/java/JavaServlets.html
	http://www.journaldev.com/1877/java-servlet-tutorial-with-examples-for-beginners
	http://www.journaldev.com/1997/servlet-example-in-java-with-database-connection-and-log4j-integration
	http://www.journaldev.com/1933/java-servlet-filter-example-tutorial

-->