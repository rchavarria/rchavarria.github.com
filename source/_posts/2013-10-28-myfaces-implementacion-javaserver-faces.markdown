---
layout: post
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
visita [http://localhost:8080/login.jsf] para disfrutar.

<!-- more -->



# Instructions

## Start with a maven webapp archetype

The fastest way to start is using a maven archetype. So, why not start using
the maven webapp archetype by default? Type the following command:

    mvn archetype:generate -DgroupId=<group-id> -DartifactId=<app-id> -DarchetypeArtifactId=maven-archetype-webapp

Where `group-id` is your group name, for example, your company name followed by 
your project name, such as `es.rchavarria.jsf`. The `app-id` is the name of
your new application. We will use `jsf-basics`.

This command will create the skeleton of a Java web application, including an
index `.jsp` page and a `web.xml` file, describing the web application. We will
modify these files and others to complete our demo.

## Add dependencies

Now it's the time to add our needed dependencies, let's start:

- `myfaces-api`: The public API classes of the Apache MyFaces CORE project.
- `myfaces-impl`: The private implementation classes of the Apache MyFaces Core 
Implementation
- `tomahawk20`: JSF components and utilities to use in a JSF 2.x implementation.
- `javax-servlet`: We will access to http request objects through the servlet
implementation.
- `jetty`: Include jetty as our server for development.

## Configure FacesServlet in webapp descriptor file.

We need to configure a servlet, the FacesServlet, to handle all JSF invocations.
To do so, we need to modify the `web.xml` file:

    <servlet>
        <servlet-name>Faces Servlet</servlet-name>
        <servlet-class>javax.faces.webapp.FacesServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>Faces Servlet</servlet-name>
        <url-pattern>*.jsf</url-pattern>
    </servlet-mapping>

Basically, it means: our servlet `Faces Servlet` will handle all requests 
ending in `.jsf`.

Most tutorials don't go further, but this configuration doesn't work. We need to
setup a servlet listener, to start MyFaces initialization. So, be sure to
include the following config:

    <listener>
        <listener-class>org.apache.myfaces.webapp.StartupServletContextListener</listener-class>
    </listener>

This is a demo, and we are under a development stage, so I would recomend to use
this context param for our servlet (see a list of lots of context params documented
in the [Apache MyFaces project](https://myfaces.apache.org/core21/myfaces-impl/webconfig.html)). 

    <context-param>
        <param-name>javax.faces.PROJECT_STAGE</param-name>
        <param-value>Development</param-value>
    </context-param>

## Create a managed bean called `login`

We will create a simple managed bean, and it will allow us to access it in our
JSF view, our first page that we will see later.

It is fairly simple, just use the annotation `@ManagedBean` and you'll get it.
We can use it, for example, to return a title for our future login form. Let's
take a look to the code:

    import javax.faces.bean.ManagedBean;

    @ManagedBean(name = "login", eager = true)
    public class GreetingBean {
        public String getMessage() {
            return "Login user";
        }
    }

We will learn how to acces this managed bean in a `.jsf` page in the next step.

## Create a view template for login page

Facelets is the default templating system in JSF 2.0, and the code is stored in 
`.xhtml` files. We can use JSF components inside this view and we can access 
managed beans (and other elements) through the Expresion Language, built in 
Java EE.

Take a look to the `login.xmtl` file under the `src/webapp` folder. You will find
something similar to this:

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

Note that we define two new namespaces: `f` and `h`. This will allow us to use
components provided by JSF.

We are getting the `h2` title from our managed bean `login` through an Expression
Language statement: `#{login.message}`. This will invoke the method `getMessage()`
of our managed bean.

The `h:commandButton` element will allow us to use the method `submit()` of our
managed bean to control the next step in the navigation model. This method is usually
known as an *action method*.

## Create another managed bean

We will create a new managed bean, called `paramReader`. Its purpouse will be to
read the request parameters and return them to a view template.

To read the parameters, we will access to the `HttpServletRequest` object through the
`FacesContext` and its `ExternalContext` object:

    public List<Parameter> getParams() {
        FacesContext fc = FacesContext.getCurrentInstance();
        HttpServletRequest request = (HttpServletRequest) fc.getExternalContext().getRequest();
        // ...      
        return params;
    }

## Create another view template

In this new view, we will handle the list of values returned by the `paramReader`
bean. JSF, by default, doesn't provide any component to handle a list of values, 
so we will use Apache Tomahawk, and its component `dataList` to handle them.

Our view, `success.xhtml`, will show the list of values in an unordered HTML list.
It would look similar to this:

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

We will use the action method `login()` in the `h:commandLink` element to navigate
back to our login page.

# Run

Run the maven command `mvn jetty:run` or just `mvn` to start the server. Then,
visit [http://localhost:8080/login.jsf] and play!.

# Further reading

- [Mojarra project](https://javaserverfaces.java.net/): 
the reference implementation of the JSF specification.
- [JSF on Wikipedia](https://en.wikipedia.org/wiki/JavaServer_Faces):
Wikipedia entry for JavaServer Faces.
- [Facelets](https://en.wikipedia.org/wiki/Facelets):
Facelets is the default templating system for JSF, instead of JSP's pages
- [MyFaces](https://myfaces.apache.org/):
an implementation developed by Apache.
- [Kinds of managed beans](http://java.dzone.com/articles/making-distinctions-between):
a comparison table of several kinds of managed beans.
