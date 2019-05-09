---
title: "Apache MyFaces como implementacion de JavaServer Faces"
date: 2013-10-28 13:12
author: Rubén Chavarría
comments: true
categories: 
- tutorials
- Java EE
- JSF
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
    Find an English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/jsf-basics">source code repository</a>.
</div>

Esta semana, en esta demo sobre Java EE escribiremos una sencilla aplicación
para conocer JavaServer Faces 2.1, un framework MVC impulsado por los 
estándares Java EE.

Será similar a otras demos. Tendremos una página de bienvenida, con un 
formulario donde el usuario podrá introducir su email y una contraseña. Los
datos del formulario se enviarán a una nueva página que mostrará los 
parámetros y sus valores enviados al servidor y permitirá navegar de vuelta
a la pantalla inicial.

Para probarla, simplemente bájate el código, ejecuta el comando `mvn` y
visita [http://localhost:8080/login.jsf](http://localhost:8080/login.jsf) para disfrutar.

<!-- more -->

## Demo

La demo será una aplicación que mostrará los parámetros enviados a través de 
una petición HTTP, y el esquema de navegación será el siguiente:

![Esquema de navegación]({{ site.baseurl }}/assets/images/2013/jsf-navigation.png)

### Comencemos con el esqueleto

La forma más rápida de comenzar es con un *archetype* de maven. Así pues,
usaremos el archetype por defecto de maven, el cual nos creará un
esqueleto inicial para comenzar con nuestra aplicación web. Escribir el 
siguiente comando:

```bash
mvn archetype:generate \
    -DgroupId=<group-id> \
    -DartifactId=<app-id> \
    -DarchetypeArtifactId=maven-archetype-webapp
```

Donde `group-id` es el nombre de grupo, por ejemplo, el nombre de la empresa
seguido por el del proyecto. Esta demo usará `es.rchavarria.jsf`. `app-id` es
el nombre que queremos para nuestra nueva aplicación, digamos `jsf-basics`.

Este comando creará el esqueleto de una aplicación web Java, e incluirá una 
primera página `.jsp` (que podemos borrar) y un descriptor de la aplicación
web, `web.xml`. Para la demo, modificaremos estos ficheros y añadiremos otros
para completarla.

### Añadimos dependencias

El siguiente paso es añadir las dependencias necesarias a nuestro proyecto:

- `myfaces-api`: el API pública de clases del proyecto core de Apache MyFaces.
- `myfaces-impl`: la implementación privada del API de Apache MyFaces Core
- `tomahawk20`: componentes y utilidades JSF para su uso con la implementación de
JSF 2.x.
- `javax-servlet`: para acceder al objeto *request* dentro de la aplicación.
- `jetty`: incluiremos `jetty` como nuestro servidor para desarrollo.

### Configurar FacesServlet en el descriptor de la applicación web

Necesitamos configurar un servlet, FacesServlet en nuestro caso, que gestione
todas las peticiones a JSF. Para ello modificaremos el fichero `web.xml` de la
siguiente forma:

```xml
<servlet>
    <servlet-name>Faces Servlet</servlet-name>
    <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>Faces Servlet</servlet-name>
    <url-pattern>*.jsf</url-pattern>
</servlet-mapping>
```

Esto hará que el servlet llamado *Faces Servlet* gestionará todas las peticiones
a páginas que terminen en `.jsf`.

La mayoría de tutoriales se quedan aquí, pero esta configuración **NO** es
suficiente. Es necesario añadir un listener a nuestro servlet, que dispare la
inicializaci´on de MyFaces. Asegúrate de incluir esto en el `web.xml`:

```xml
<listener>
    <listener-class>org.apache.myfaces.webapp.StartupServletContextListener</listener-class>
</listener>
```

Estamos en una demo, y por lo tanto bajo un entorno de desarrollo, por lo que 
recomendaría usar un *context param* para indicarselo a MyFaces. 

```xml
<context-param>
    <param-name>javax.faces.PROJECT_STAGE</param-name>
    <param-value>Development</param-value>
</context-param>
```

Para ver una lista completa de parámetros que podemos usar, no dejes de leer la 
documentacón sobre cómo 
[configurar MyFaces](https://myfaces.apache.org/core21/myfaces-impl/webconfig.html).

### Crear una *managed bean* llamada `login`

Crearemos una *managed bean*, que no es más que un POJO que será inyectado en 
nuestra vista de JSF y podremos acceder a sus getters/setters y otros métodos.

Crearla es realmente sencillo, usaremos la anotación `@ManagedBean` y ya estará
casi todo hecho. Como primer uso, haremos que devuelva un título para nuestro
futuro formulario de login. Es un caso de uso muy sencillo, pero nos servirá para
conocer la potencia de JSF. Un vistazo al código:

```java
import javax.faces.bean.ManagedBean;

@ManagedBean(name = "login", eager = true)
public class GreetingBean {
    public String getMessage() {
        return "Login user";
    }
}
```

En el próximo paso, veremo cómo acceder a esta managed bean.

### Crear una vista para la página de login

[Facelets] es el sistema de plantillas por defecto en JSF 2.0 (y posteriores).
Esto supone que el código de la vista es XML y se guarda en ficheros con la
extensión `.xhtml`. Podemos usar componentes JSF dentro de esta vista así como
acceder a managed beans a través del Expression Language, proporcionado por el
estándar Java EE.

Gracias a que las vistas son *plantillas*, podemos crear componentes visuales
con ellas y reutilizarlos a lo largo de nuestro proyecto.

Aquí muestro un extracto de nuestra vista de login, el fichero `login.xhtml` que
se encuentra en el directorio `src/webapp`:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
   "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:f="http://java.sun.com/jsf/core"
      xmlns:h="http://java.sun.com/jsf/html">
<!-- ... -->
      <h:form styleClass="form-signin">
        <h2>#{login.message}</h2>

        <h:commandButton id="login" value="Log me in" 
                         styleClass="btn btn-lg btn-primary btn-block"
                         action="#{login.submit}" />
      </h:form>
</html>
```

Nótese que se han definido dos nuevos *namespaces*: `f` y `h`. Esto nos permitirá
usar componentes reutilizables proporcionados por JSF.

En el código vemos que tomamos el título `h2` de la managed bean llamada `login`
a través de una sentencia de Expression Language: `#{login.message}`. Esto 
invocará al método `getMessage()` definido en nuestra managed bean.

El elemento `h:commandButton` nos permite usar el método `submit()` de la managed
bean para controlar el siguiente paso a dar en nuestro modelo de navegación. Este
tipo de métodos se conocen como *action method*. Devuelven una `String`, la cual
identifica la siguiente vista a renderizar.

### Una nueva managed bean

Crearemos una nueva managed bean, llamada `paramReader`. Su propósito será el de 
leer los parámetros de la petición HTTP enviada desde la vista anterior y 
devolver estos parámetros en forma de lista de valores a una nueva vista.

Para leer los parámetros, lo haremos a través del objeto `HttpServletRequest`,
all cual accederemos a través de `ExternalContext` del `FacesContext`, del
siguiente modo:

```java
  public List<Parameter> getParams() {
      FacesContext fc = FacesContext.getCurrentInstance();
      HttpServletRequest request = (HttpServletRequest) fc.getExternalContext().getRequest();
      // ...      
      return params;
  }
```

### Crear una nueva vista

En esta nueva vista, manipularemos la lista de valores devueltos por la 
managed bean `paramReader`. Por defecto, JSF no proporciona ningún componente
para manipular listas de datos, por lo que aquí usaremos [Apache Tomahawk] y
su componente `dataList`.

Nuestra nueva vista, `success.xhtml`, mostrará lal lista de valores en un elemento
HTML. El código (parcial) será algo parecido a esto:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
   "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:h="http://java.sun.com/jsf/html"
      xmlns:t="http://myfaces.apache.org/tomahawk">
<!-- ... -->
      <ul>
        <t:dataList var="aParam"
                    value="#{paramReader.params}">
          <li>
            <h:outputText value="#{aParam.key}" /> :
            <h:outputText value="#{aParam.value}" />
          </li>
        </t:dataList>
      </ul>

      <h:form>
        <h:commandLink action="#{paramReader.login}">Back to login page</h:commandLink>
      </h:form>
</html>
```

Usaremos el action method `login()` en el elemento `h:commandLink` para permitir al
usuario navegar de vuelta al la página de login.

## Ejecutar

Para ver la demo en acción, simplemente ejecutar el comando maven `mvn jetty:run`.
Esto arrancará el servidor. Después, visita la URL 
[http://localhost:8080/login.jsf](http://localhost:8080/login.jsf) y a jugar!.

## Enlaces y referencias

- [Mojarra project](https://javaserverfaces.java.net/): 
the reference implementation of the JSF specification.
- [JSF on Wikipedia](https://en.wikipedia.org/wiki/JavaServer_Faces):
Wikipedia entry for JavaServer Faces.
- [Facelets](https://en.wikipedia.org/wiki/Facelets): Facelets is the default templating system for JSF, instead of JSP's pages
- [MyFaces](https://myfaces.apache.org/):
an implementation developed by Apache.
- [Apache Tomahawk](http://myfaces.apache.org/tomahawk/index.html): componentes y utilidades JSF para su uso con la implementación de
JSF 2.x.
- [Kinds of managed beans](http://java.dzone.com/articles/making-distinctions-between):
a comparison table of several kinds of managed beans.

[Facelets]: https://en.wikipedia.org/wiki/Facelets
[Apache Tomahawk]: http://myfaces.apache.org/tomahawk/index.html
