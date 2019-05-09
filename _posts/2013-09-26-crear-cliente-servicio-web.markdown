---
title: "Crear una applicación cliente para un servicio web"
date: 2013-09-26 07:41
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
    Find a lightweight English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/ws-jaxws-client">source code repository</a>.
</div>

En esta demo crearemos un cliente para el servicio web desarrollado en la demo
anterior. Para ello, utilizaremos una herramienta proporcionada por Java para 
generar unas clases a partir del fichero WSDL de descripción del servicio web, y
usaremos dichas clases para invocar el servicio. Así de fácil.

Se puede ver el código fuente de la demostración en el directorio 
[`ws-jaxws-client`](https://github.com/rchavarria/javaee-6-demos/tree/master/ws-jaxws-client)
del repositorio de las demos en github.

<!-- more -->

## Demo

Esta demo pertenece a una serie de 
[tutoriales de demostración de tecnologías J2EE]({{ site.baseurl }}{% post_url 2013-09-03-demos-tecnologias-javaee %}) y 
en esta en particular crearemos en cliente que invocará a los métodos expuestos por el servicio
web desarrollado en la demo anterior. Estos métodos son:

1. Añadir usuario: añadiremos un nombre de usuario al servicio.
2. Obtener usuario: mediante un identificador, obtendremos un nombre de usuario.

Con lo cual, añadiremos y consultaremos usuarios.

## Pasos a seguir

### Arrancar el servicio web

Lo primero que debemos hacer es arrancar nuestro servicio web. Es necesario para que
el fichero WSDL, que describe el servicio, esté disponible y actualizado. También
es posible usar un fichero ya existente, por ejemplo, en el caso de que queramos
desarrollar un cliente para un servicio web de terceros. En definitiva, el elemento
realmente importante en un servicio web, es el fichero WSDL, que es quien define 
de manera inequívoca el servicio en sí. 

Para esta demo, arrancaremos el servicio web desarrollado en la
[demo anterior](/blog/2013/09/19/crear-servicio-web-jaxws). Básicamente, los comandos
para arrancarlo, partiendo del directorio raíz del código fuente de todas las demos:

```
cd ws-jaxws-cxf
mvn jetty:run
```

De esta forma tendremos el fichero WSDL disponible en `http://localhost:8080/Users?wsdl`.

### Generar las clases necesarias con `wsimport`

Java proporciona una herramienta, `wsimport`, que genera las clases necesarias
para poder consumir fácilmente un servicio web a partir de un fichero WSDL.

La sintaxis del comando es:

```bash
wsimport [options] <WSDL_URI>
```

Así, en nuestro caso, un ejemplo sería:

```bash    
wsimport http://localhost:8080/Users?wsdl
```

Este comando genera las clases, las compila y borra el código fuente. Esto no es 
muy práctico a la hora de aprender, así que usaremos algunas opciones para
obtener el código fuente de las clases generadas.

- `-d src/main/java`: indica el directorio donde queremos generar las clases.
- `-keep`: mantiene los ficheros `.java` generados.
- `-Xnocompile`: no compila los fuentes generados, ya se encargará nuestra 
herramienta de ello, no os preocupéis.

El comando completo quedaría:

```bash
wsimport -d src/main/java -keep -Xnocompile http://localhost:8080/Users?wsdl
```

Las clases generadas que más nos importan, son:

- `UsersManagementService`: esta clase representa el servicio web en sí.
- `UsersManagement`: esta clase contiene los mismos métodos que el servicio web
definido por el fichero WSDL, y actúa como un proxy a la hora de invocar a nuestro
servicio. A esta clase se le denomina `port` (puerto), y es quien nos permite llamar
a los _métodos_ web.

### Crear un test de JUnit para invocar el servicio web

![Ejecución de la demo como un test]({{ site.baseurl }}/assets/images/2013/web-service-test.png)

Usaremos un sencillo test de JUnit para invocar a nuestro servicio. Se puede utilizar
una clase normal de Java, con un método `main`, pero haciéndolo con un test, podemos
integrar su ejecución en el ciclo de vida del proyecto gestionado por `maven` y
ejecutarlo muy fácilmente con `mvn test`.

Antes de nada, es necesario añadir la dependencia de JUnit a nuestro proyecto:

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.8.1</version>
    <scope>test</scope>
</dependency>
```

Crearemos el test en el paquete `es.rchavarria.ws.client`. En el método `setUp`
de nuestro test (el que se ejecutará antes que cualquier test) crearemos una
instancia del servicio, y a través de él, obtendremos una instancia de nuestra
clase _port_. Esta clase será quien nos permita invocar al servicio web.

```java
//...
public class JaxWsClientTest {

    private UsersManagement port;

    @Before
    public void setUp() {
        UsersManagementService service = new UsersManagementService();
        port = service.getUsersManagementPort();
    }

//...        
}
```

### Invocando el servicio web

Ahora ya disponemos de la clase _port_, así que ya somos capaces de invocar los
métodos expuestos por el servicio: `addUser` y `getUser`. A por ellos!!

```java
@Test
public void test() {
    assertEquals(1, port.addUser("The boss"));
    assertEquals(2, port.addUser("The king"));
    assertEquals(3, port.addUser("The queen"));
    
    assertEquals("The boss", port.getUser(1));
    assertEquals("The queen", port.getUser(3));
    assertEquals("The king", port.getUser(2));
}
```

## Ejecución

Esta demo se puede ejecutar como un test de JUnit, y estaría integrado en la ejecución
de `maven`, así que simplemente ejecuta el comando `mvn test` para ver los resultados.

He añadido también un plugin, surefire report, por lo que ejecutnado el comando 
`mvn site`, la herramienta generará (entre otras cosas), un informe con los resultados
de la ejecución de nuestros tests. Ejecuta el comando y abre el fichero HTML que 
encontrarás en esta ruta dentro del directorio raiz del proyecto `target/site/index.html`.

## Enlaces para ampliar información

- [Building web services with JAX-WS](http://docs.oracle.com/javaee/6/tutorial/doc/bnayl.html)
- [Building RESTful Web Services with JAX-RS](http://docs.oracle.com/javaee/6/tutorial/doc/giepu.html)
