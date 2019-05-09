---
title: "Crear un servicio web JAX-WS"
date: 2013-09-19 08:49
comments: true
categories: 
- tutorials
- Java EE
- programming
- web service
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
    Find a lightweight English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/ws-jaxws-cxf">source code repository</a>.
</div>

En esta demo crearemos un servicio web. Básicamente existen dos tipos de servicios
web: SOAP, basados en el intercambio de mensajes XML; y servicios web basados en 
una interfaces REST, RESTful web services.

Aquí crearemos un servicio web SOAP, el cual establece que los mensajes XML pueden ser
transportados por diversos protocolos, aquí lo haremos sobre HTTP, ya que es lo más
común y sencillo. Ya que usaremos HTTP como protocolo de transporte, nuestro servicio web estará 
gestionado por un servlet.

Se puede ver el código fuente de la demostración en el directorio 
[`ws-jaxws-cxf`](https://github.com/rchavarria/javaee-6-demos/tree/master/ws-jaxws-cxf)
del repositorio de las demos en github.

<!-- more -->

## Demo

![Foto por el usuario de flickr psd]({{ site.baseurl }}/assets/images/2013/web-services-by-psd.jpg)

En esta demo no veremos nada funcionando, ya que vamos a crear un servicio web
pero no vamos a crear un cliente que lo consuma (eso para la siguiente). La forma
de comprobar que hemos creado un servicio web correcto será la visualización del
fichero WSDL generado por el servicio, el cual es el contrato entre el proveedor
del servicio (lo creado en esta demo) y el consumidor del mismo (el cliente que
crearemos más adelante).

La funcionalidad que nos ofrecerá el servicio se apoyarán en dos métodos:

1. Añadir usuario: añadiremos un nombre de usuario al servicio.
2. Obtener usuario: mediante un identificiador, obtendremos un nombre de usuario.

Para ejecutar la demo, simplemente hay que descargase el código fuente y ejecutar
`mvn jetty:run` desde el directorio raiz de la demo. Visitar la página de login
[http://localhost:8080/Users?wsdl](http://localhost:8080/Users?wsdl) y veremos
el fichero WSDL con la definición del servicio.

## Pasos a seguir

### Elegir un framework que implemente JAX-WS

Según la [documentación de Oracle](http://docs.oracle.com/javaee/6/tutorial/doc/bnayl.html),
crear un servicio web parece realmente 
sencillo y para toda la familia. Lo que no explican es que están dependiendo
de la implementación de los servicios web incluída en *su* contenedor Java EE,
Glassfish. No tengo nada en contra, pero me gusta tener cierta independencia,
por lo que vamos a elegir otro framework que implemente la especificación
JAX-WS.

He elegido [Apache CXF](http://cxf.apache.org), aunque hay otras implementaciones 
disponibles, como [Spring WS](http://projects.spring.io/spring-ws/)
(quizá en un futuro, veamos su uso).

### Dependencias del proyecto maven

Como todas las demos, utilizaremos `maven` como gestor del ciclo de vida del
proyecto, y las dependencias son una parte muy importante de la vida del proyecto.

La aplicación depende de:

- `javax.servlet-api`: el API de Java EE para servlets, ya que será un servlet
quien gestione las peticiones HTTP. Nuestro servicio web se basará en este servlet.
- `cxf-rt-frontend-jaxws`: la implementación de CXF de la especificación JAX-WS.
- `cxf-rt-transports-http`: HTTP será el protocolo de transporte.
- `spring-web`: CXF usa Spring internamente para su funcionamiento.

### Crear el interfaz del servicio

Nuestro servicio web servirá para almacenar nombres de usuarios, y se podrán 
recuperar estos nombres a través de un identificador que devolverá el servicio
al añadirlos.

Por lo tanto, vemos que necesitaremos dos métodos:

- `addUser`: para añadir un usuario al sistema.
- `getUser`: para recuperar un nombre de usuario.

Nuestro interfaz de servicio sería algo así:

```java
import javax.jws.WebService;
import javax.jws.WebParam;

@WebService
public interface UsersManagement {
    public String getUser(@WebParam(name="userId") int userId);
    public int addUser(@WebParam(name="name") String name);
}
```

### Crear la implementación del servicio

Ya tenemos la definición del servicio, ahora debemos implementarlo. Esta
implementación deberá estar anotada también con `@WebService`, y deberemos
proporcionar valores a algunos parámetros de la anotación. El más importante
es `endpointInterface`, que debe apuntar a la definición del servicio.

La implementación tendrá un aspecto similar a éste:

```java
import javax.jws.WebService;

@WebService(endpointInterface = "es.rchavarria.ws.UsersManagement",
            serviceName = "Users")
public class UsersManagementImpl implements UsersManagement {
     // ... implementación de los métodos
}
```

Invito a bucear en el código para ver la implementación de los métodos,
aunque no es muy interesante de ver, todo sea dicho.

### Establecer un servlet que gestione las peticiones HTTP

El siguiente paso es establecer un servlet que gestione las peticiones HTTP.
Apache CXF nos proporciona dicho servlet, por lo que deberemos configurar
nuestro contenedor Java EE para que lo arranque. El servlet gestionará todas
las peticiones, con lo que estableceremos el patrón URL a `/*`.

Es muy importante que el patrón URL del servlet sea capaz de gestionar la URL
donde se despliegue el servicio web, en caso contrario, las peticiones no
llegarán al servicio web. Por ejemplo, si el patrón URL del servlet es
`/services/*` y nuestro servicio web se despliega en `/web-services/*`,
las peticiones a nuestro servicio no serán gestionadas por el servlet.

Para establecer el servlet, creamos un fichero descriptor de la aplicación web,
`web.xml`:

```xml
<servlet>
    <servlet-name>the-cxf-servlet</servlet-name>
    <servlet-class>org.apache.cxf.transport.servlet.CXFServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>the-cxf-servlet</servlet-name>
    <url-pattern>/*</url-pattern>
</servlet-mapping>
```

### Configurar el servlet de CXF

El servlet de CXF arrancará con el servidor, pero no sabe qué servicios web puede
invocar. Debemos configurarlo. CXF proporciona un mecanismo para ello, a través
de un fichero XML.

Podríamos utilizar un fichero por defecto, y guardarlo en `WEB-INF/cxf-servlet`,
o podemos configurarlo manualmente. Lo haremos de forma manual, e indicaremos al
servlet donde está su fichero de configuración. Se lo indicaremos a través de un
parámetro de inicialización de servlet, por lo que modificaremos nuestro `web.xml`:

```xml
<!-- ... -->
<servlet>
    <servlet-name>the-cxf-servlet</servlet-name>
    <servlet-class>org.apache.cxf.transport.servlet.CXFServlet</servlet-class>

    <init-param>
        <param-name>config-location</param-name>
        <param-value>/WEB-INF/services.xml</param-value>   
    </init-param>        

    <load-on-startup>1</load-on-startup>
</servlet>
<!-- ... -->
```

También debemos añadir el fichero de configuración del servlet CXF, el cual hemos
llamado `WEB-INF/services.xml`: 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:jaxws="http://cxf.apache.org/jaxws"
      xmlns:soap="http://cxf.apache.org/bindings/soap"
      xsi:schemaLocation="
http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
http://cxf.apache.org/bindings/soap http://cxf.apache.org/schemas/configuration/soap.xsd
http://cxf.apache.org/jaxws
http://cxf.apache.org/schemas/jaxws.xsd">

  <jaxws:server id="aServer" serviceClass="es.rchavarria.ws.UsersManagement" address="/Users">
    <jaxws:serviceBean>
        <bean class="es.rchavarria.ws.UsersManagementImpl" />
    </jaxws:serviceBean>
  </jaxws:server>
</beans>
```

Esto es un fichero de configuración de Spring, y es que CXF usa Spring internamente. Se
añade un nuevo namespace, `jaxws`, proporcionado por CXF y que viene con etiquetas XML
para configurar un servidor que responda a las peticiones dirigidas a nuestro servicio web.

### Listos

La demo ya está lista para ser ejecutada. Si la ejecutamos con el comando `mvn jetty:run`
podremos visitar [http://localhost:8080/Users?wsdl](http://localhost:8080/Users?wsdl) 
y veremos el fichero WSDL que define el servicio web.

En la próxima demo, crearemos un cliente a partir de este fichero WSDL, y comprobaremos
cómo funciona.

## Código fuente

Para echar un ojo al código fuente, visitar el directorio 
[`ws-jaxws-cxf`](https://github.com/rchavarria/javaee-6-demos/tree/master/ws-jaxws-cxf).

## Enlaces para ampliar información

- [Construir servicios web con JAX-WS](http://docs.oracle.com/javaee/6/tutorial/doc/bnayl.html)
- [Construir servicios web REST con JAX-RS](http://docs.oracle.com/javaee/6/tutorial/doc/giepu.html)
- [Guía de uso de Apache CXF](http://cxf.apache.org/docs/index.html)

*Imagen obtenida de [psd](http://www.flickr.com/photos/psd)*
 