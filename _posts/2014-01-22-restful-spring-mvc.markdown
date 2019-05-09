---
title: "Aplicacion web RESTful con Spring MVC"
date: 2014-01-22 23:10
author: Rubén Chavarría
comments: true
categories: 
- tutorials
- Java EE
- Spring MVC
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
    Find an English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/spring-mvc">source code repository</a>.
</div>

En esta demo crearemos una aplicación web para demostrar el uso del framework
Spring MVC para crear servicios REST.

![Spring MVC]({{ site.baseurl }}/assets/images/2014/spring-mvc.png)

Será una aplicación web sencilla, sin persistencia en base de datos (para no
complicarla), pero será una aplicación Spring MVC completa donde, en lugar de
generar las respuestas mediante páginas JSP, éstas serán generadas en formato
JSON, para ser consumidas como si se trataran de servicios web.

<!-- more -->

La aplicación no será un servicio web, estrictamente hablando, pero responderá a
peticiones HTTP `get`, `post`, `put` y `delete` como si se tratara de uno de ellos.

# Instrucciones

La aplicación será la típica que ofrece operaciones [CRUD](https://es.wikipedia.org/wiki/CRUD),
y gestionará una lista de casas, pisos, chalets,... Es decir, los tipos de propiedades 
gestionadas por una agencia inmobiliaria. Por eso, nuestra entidad, nuestro 
recurso (hablando en terminología REST), será una Propiedad o `Property`.

Veamos los distintos pasos que daremos para desarrollar la aplicación:

## Definir la URI para acceder a nuestra entidad

Solamente tendremos un recurso al que acceder, una Propiedad, así que solo
tendremos una URI a la que acceder:

```
http://<server name>/springmvc/properties
```

Debemos definir los métodos HTTP que usaremos para gestionar las Propiedades:

- `GET /properties`: devolverá una lista de Propiedades
- `GET /properties/{id}`: devolverá los detalles de una Propiedad identificada por {id}
- `POST /properties`: creará una nueva Propiedad
- `DELETE /properties/{id}`: borrará una Propiedad
- `PUT /properties/{id}`: actualizará una Propiedad

# Crear un controlador MVC de consultas

El controlador, que responderá a peticiones de consulta (listar y obtener
por id), se llamará 
`es.rchavarria.springmvc.rest.PropertiesQueriesController`.

Responderá a peticiones HTTP que consulten datos, tales como listar las Propiedades u
obtener los detalles de una de ellas.

Debemos marcar el controlador con anotaciones de Spring MVC de forma que Spring
reconozca la clase como controlador MVC. Usaremos las anotaciones para indicar
qué URI gestionará. Nuestro controlador vacío podría ser algo así:

```java
    @Controller
    @RequestMapping("/properties")
    public class PropertiesQueriesController {
    }
```

## Crear un método que liste Propiedades

Nuestro primer método será uno que devuelva una lista de Propiedades. La lista
será creada/obtenida/generada por un servicio, no por el controlador en sí 
mismo. En un principio, el servicio gestionará las Propiedades sin ningún tipo
de persistencia, pero siempre podremos implementarla en un futuro.

El método mapeará el método `get` de HTTP y su valor retornado será parte del 
cuerpo de la respuesta. De esta forma, la respuesta no será generada por una
página JSP, sino que la respuesta será texto en formato JSON generado
a partir de un objeto Java:

```java
    @RequestMapping(method = RequestMethod.GET)
    @ResponseStatus(HttpStatus.OK)
    @ResponseBody
    public List<String> getAllProperties() {
        return Arrays.asList("one", "two", "three");
    }
```

## Crear tests para probar el controlador

Este test será un test de integración, ya que no podemos considerarlo como un
test unitario. No lo podemos considerar así ya que el test arrancará un pequeño
servidor web, arrancará nuestro controlador y realizará peticiones HTTP reales
contra él (un test unitario no debería hacer tantas tareas).

Usaremos [Mockito](https://code.google.com/p/mockito/) para simular dependencias
externas y un componente proporcionado por Spring MVC, `MockMVC`. Este componente
será el servidor y gestionará las peticiones y analizará las respuestas de
nuestro controlador.

El siguiente código muestra cómo preparar un servidor y cómo configurar nuestro
controlador en él: 

```java
    // ...

    private MockMvc mockMvc;

    @InjectMocks
    PropertiesQueriesController controller;

    @Mock
    PropertyService propertyService;

    @Before
    public void setup() {
        MockitoAnnotations.initMocks(this);

        mockMvc = standaloneSetup(controller)
                .setMessageConverters(new MappingJackson2HttpMessageConverter())
                .build();
    }

    // ...
```

Y en el siguiente código vemos cómo probar una petición HTTP `get`:

```java
    @Test
    public void testRequestAllPropertiesUsesHttpOK() throws Exception {
        when(propertyService.requestAllProperties()).thenReturn(allProperties());

        mockMvc.perform(get("/properties")
            .accept(MediaType.APPLICATION_JSON))
            .andExpect(status().isOk());
    }
```

Crearemos otro test, para comprobar esta vez que el resultado es el esperado:

```java
    @Test
    public void testRequestAllPropertiesRendersOkAsJSON() throws Exception {
        when(propertyService.requestAllProperties()).thenReturn(allProperties());

        mockMvc.perform(get("/properties")
            .accept(MediaType.APPLICATION_JSON))
            .andDo(print())
            .andExpect(jsonPath("$[0].city").value("first city"))
            .andExpect(jsonPath("$[1].address").value("second address"))
            .andExpect(jsonPath("$[2].price").value(300));
    }
```

Para ver más tests o los tests al completo, por favor, echa un vistazo al 
[código de la demo](https://github.com/rchavarria/javaee-6-demos/tree/master/spring-mvc)
en github.

## Añadir un método al controlador que acepte un parámetro en la URI

Usaremos URIs del tipo `http://<server>/springmvc/properties/<id>` para obtener los
detalles de una Propiedad en concreto. `<id>` representa un identificador de Propiedad,
y el controlador deberá devolver los detalles de la misma en lugar de una lista con
todas las propiedades.

En el controlador, anotaremos un nuevo método con `@RequestMapping` la cual tendrá
dos parámetros: `method`, será el método HTTP `get`; y `value`, para dar un nombre al 
parámetro. La anotación `@ResponseStatus` indica al framework el código de estado 
HTTP que deberá devolver y `@ResponseBody` nos indica que el valor devuelto por el 
método debe ser el cuerpo de mensaje de respuesta.

Este nuevo método tendrá un parámetro, anotado con `@PathVariable`. Esta anotación
mapea los parámetros del método con parámetros en la URI.

```java
    @RequestMapping(method = RequestMethod.GET, value="/{id}")
    @ResponseStatus(HttpStatus.OK)
    @ResponseBody
    public Property getProperty(@PathVariable String id) {
        return propertyService.findById(id);
    } 
```

Crearemos un test similar al anterior test de integración, pero para no hacer eterno
este post, prefiero que le eches un vistazo al código en el 
[proyecto de github](https://github.com/rchavarria/javaee-6-demos/tree/master/spring-mvc).

## Configurar controladores MVC

Usaremos anotaciones para configurar nuestros controladores, Spring MVC lo hace 
extremadamente fácil y proporciona una anotación, `@EnableWebMVC`, que hace
prácticamente todo por nosotros. Y esto es casi todo lo que hay que hacer para
configurar una aplicación MVC.

Nuestra configuración está centralizada en una clase, la cual será sencillísima
y se parecerá a ésta:

```java
    @Configuration
    @EnableWebMvc
    @ComponentScan(basePackages = { "es.rchavarria.springmvc.rest.controllers" })
    public class MVCConfig {}
```

También crearemos un test de integración para comprobar que configuramos bien
nuestros controladores. Busca el test `MVCConfigIntegrationTest` en el 
[repositorio de código](https://github.com/rchavarria/javaee-6-demos/tree/master/spring-mvc)
para verlo.

## Inicializar la aplicación web

Seguiremos sin usar ficheros XML para configurar nuestra aplicación, por lo que lo haremos
a través del código. 

Crearemos una clase que herede de una proporcionada por Spring, 
`AbstractAnnotationConfigDispatcherServletInitializer`,
y sobreescribiremos los siguientes métodos:

- `getRootConfigClasses`: debe devolver un array de clases que configuren el contexto raíz
(root context). Por ahora, no tenemos tal cosa, por lo que puede devolver un array 
vacío o simplemente el valor `null`.
- `getServletConfigClasses`: debe devolver un array de clases que configuren el
contexto servlet.
- `getServletMappings`: debe devolver los mapeos del servlet.

Ya estamos listos para ejecutar nuestra demo en un contenedor de servlets. En este caso,
ejecutaremos la aplicación en un servidor Tomcat 7. Para ello, añadiremos el plugin de 
maven de Tomcat 7 a nuestro fichero `pom.xml`...

```xml
    <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
    </plugin>
```

... y ejecutaremos la aplicación con el comando `mvn tomcat7:run`.

## ¿Por dónde seguir?

Este post ya ha quedado demasiado largo para publicarse, pero no he encontrado forma de 
hacerlo más corto y contar todos los pasos involucrados para este desarrollo, pero todavía
tenemos muchísimo trabajo por hacer, por lo que animo a visitar el repositorio de 
código fuente de la demo. 

Algunas tareas que quedan pendientes, podrían ser:

- Crear un nuevo controlador, un controlador de comandos (en contraposición a controlador de
consulta), que permita al usuario a crear, actualizar o borrar una Propiedad.
- Crear tres métodos en el controlador, uno por cada acción (crear, actualizar y borrar).
- Recuerda, cada método deberá estar probado por un test unitario o de integración, que no
se te olvide.

# Recursos y lecturas

- [Build RESTful services with Spring](http://spring.io/guides/tutorials/rest)
- [Source code of this demo](https://github.com/rchavarria/javaee-6-demos/tree/master/spring-mvc)
