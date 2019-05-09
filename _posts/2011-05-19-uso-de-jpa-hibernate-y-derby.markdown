---
title: "Uso de JPA, hibernate y derby"
date: 2011-05-19 09:44
author: Rubén Chavarría
categories: 
- derby
- apache
- base de datos
- jpa
- hibernate
comments: true
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
  <p>Este post pertenece a mi antiguo blog en <a href="http://rchavarria.wordpress.com">wordpress</a>, pero decidí pasarme a github:pages por las siguientes <a href="/blog/2012/12/03/por-que-cambie-mi-blog-en-wordpress-com">razones</a></p>
</div>

Tengo una pequeña aplicación en la que uso Apache Derby como base de datos para guardar 
los datos.

Hasta ahora, estaba utilizando el patrón DAO para guardar los datos que quería hacer 
persistentes en la aplicación. Cada clase DAO se encargaba de crear, borrar, editar y 
actualizar un tipo de datos. Estas operaciones las hacía mediante SQL puro y duro. No 
es que el modelo de datos que utilizo sea muy complicado, pero es tedioso editar 
consultas SQL para cada tipo de dato que quieres persistir.

Así pues, decidí que debería utilizar algo un poco más elaborado. Java dispone de la 
Java Persistence API, así que, ¿porqué no usarla? Y este post describe los primeros 
pasos a dar para utilizar JPA en una aplicación.

<!-- more -->

JPA es una definición, por sí sola no hace nada, necesita de una implementación para 
realizar realmente el trabajo. Existen varias implementaciones (ver 
[comparativa](http://terrazadearavaca.blogspot.com/2008/12/jpa-implementations-comparison.html)).
De todas ellas he elegido Hibernate. Puede que no sea la mejor, puede que no sea la 
más rápida o la más eficiente, pero creo que es la más conocida y la referencia para 
el resto de implementaciones.

## El ejemplo, paso a paso

Nuestro ejemplo va a consistir en algo muy (pero que muy) sencillo, pero que nos va a 
permitir aprender cómo configurar hibernate con nuestra base de datos derby. Nuestros 
datos a guardar van a ser objetos de la clase Person, que va a tener un nombre. No va 
a haber relaciones con ningún otro objeto, así que sólo exisitirá una tabla en la base 
de datos. Más sencillo, imposible.

### Datos que serán persistentes

Como ya hemos visto, sólo vamos a persistir objetos de la clase Person, la cual tendrá 
un campo `id`, que funcionará como la clave principal de la tabla, y un campo `name`, el 
nombre de la persona. A continuación vemos el código de esta clase:

```java
package es.rct.jpa.model;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
public class Person {
    @Id
    @GeneratedValue
    private long id;
    private String name;

    public void setName(final String name) {this.name = name;}
    public String getName() {return name;}
    public void setId(final long id) {this.id = id;}
    public long getId() {return id;}
}
```

De esta clase vamos a destacar 3 anotaciones, pertenecientes a JPA. Las podemos 
encontrar en el paquete `javax.persistence`:

- `Entity`: indica que esta clase es una entidad, lo cual significa que esta clase tiene 
correspondencia con una tabla en la base de datos
- `Id`: indica qué campo de la clase va a ser utilizado como clave primaria de la tabla 
representada por la entidad
- `GeneratedValue`: indica que la clave va a ser generada automáticamente por el motor 
de persistencia (hibernate)

### Dependencias de Maven

Para poder usar Derby como base de datos y Hibernate como implementación de JPA, 
debemos incluir las siguientes dependencias en nuestro fichero `pom.xml` de configuración 
de maven:

```xml
<!-- ... -->
<dependency>
    <groupId>org.apache.derby</groupId>
    <artifactId>derby</artifactId>
    <version>10.6.2.1</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-entitymanager</artifactId>
    <version>3.4.0.GA</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
<!-- ... -->
```

Las versiones de las dependencias pueden variar. Aquí aparecen las que yo personalmente 
he utilizado.

### Configurar JPA / Hibernate / Derby

Para configurar JPA, debemos escribir la configuracion en un fichero llamado 
`persistence.xml`, en un directory META-INF, accesible desde el directorio de trabajo 
de nuestra aplicación. 

Yo lo he creado en `src/main/resources/META-INF/persistence.xml`, ya que maven empaqueta el 
contenido del directorio `src/main/resources` en el jar de la aplicación, con lo que tenemos 
el resultado deseado.

El contenido del fichero de configuración JPA es el siguiente:

```xml
<persistence xmlns="http://java.sun.com/xml/ns/persistence" version="1.0">
    <persistence-unit name="test-jpa" transaction-type="RESOURCE_LOCAL">
     
    <provider>org.hibernate.ejb.HibernatePersistence</provider>
     
    <class>es.rct.jpa.model.Person</class>
    <exclude-unlisted-classes>true</exclude-unlisted-classes>
     
    <properties>
        <property name="hibernate.connection.url" value="jdbc:derby:memory:testing-jpa;create=true" />
        <property name="hibernate.connection.driver_class" value="org.apache.derby.jdbc.EmbeddedDriver" />
        <property name="hibernate.dialect" value="org.hibernate.dialect.DerbyDialect" />
        <property name="hibernate.hbm2ddl.auto" value="create" />
        <property name="hibernate.connection.username" value="" />
        <property name="hibernate.connection.password" value="" />
    </properties>
     
    </persistence-unit>
</persistence>
```

De este fichero xml podemos destacar las siguientes etiquetas:

- `persistence-unit`, atributo `name`: define una unidad de persistencia, es 
obligatorio darle un nombre, para poder crear un `EntityManager` en nuestra 
aplicación. El `EntityManager` es el encargado de manejar la persistencia de 
nuestros datos
- `provider`: aquí indicamos que queremos usar Hibernate como implementación de JPA
- `class`: debe existir una etiqueta class por cada clase que queramos persistir, 
es decir, una por cada entidad que formará nuestra unidad de persistencia
- Dentro de las etiquetas properties, definimos propiedades propietarias de la 
implementación JPA. De entre ellas cabe destacar:
    - `hibernate.connection.url`: define la URL de conexión a la base de datos. 
    Aquí estamos configurando Derby como base de datos. Estamos creando una base 
    de datos llamada "testing-jpa" en memoria (no en disco)
    - `hibernate.dialect`: configuramos Hibernate para que *hable* con Derby

### Crear un test para probar el funcionamiento

Ahora sólo queda crear nuestro código para almacenar algunos objetos del tipo `Person`.

Primero, debemos crear un objeto `EntityManager`, que manejará todo lo relacionado 
con la persistencia: transacciones, guardar datos, actualizarlos, borrarlos, etc.

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("test-jpa");
EntityManager em = emf.createEntityManager();
```

Una vez terminemos de utilizar nuestro `EntityManager`, debemos cerrarlo:

```java
em.close();
emf.close();
```

Ahora ya disponemos de un objeto `em` para poder persistir objetos de tipo `Person`:

```java
private void insertSomeData() {
    Person p = new Person();
    p.setName("person 01");
    Person p1 = new Person();
    p1.setName("person 02");

    em.getTransaction().begin();
    em.persist(p);
    em.persist(p1);
    em.getTransaction().commit();
}
```

Para poder guardar los datos en base de datos, debemos arrancar una transacción, llamar 
al método `persist` y terminar la transacción. Si queremos indicar que ha habido un 
error durante la transacción, y no queremos llevarla a cabo, llamaríamos al método 
`rollback` en lugar del método `commit`.

Para comprobar que realmente hemos almacenado los objetos en la base de datos, sólo 
tenemos que buscarlos por identificador. Ya que sólo hemos almacenado 2 objetos, y 
son los 2 primeros, los ids serán 1 y 2 respectivamente:

```java
private void listInsertedData() {
    em.getTransaction().begin();
    for (long i = 1; i <= 2; i++) {
        Person pFinded = em.find(Person.class, new Long(i));
        System.out.println("Id: " + i + ", name: " + pFinded.getName());
    }
    em.getTransaction().commit();
}
```

## Código fuente del ejemplo

Puedes descargar/ver el código fuente en este repositorio de github: 
[https://github.com/rchavarria/JPAHibernateDerby](https://github.com/rchavarria/JPAHibernateDerby)

## Referencias

Si quieres profundizar en el tema, aquí dejo unos enlaces que me han sido de gran ayuda.

- [Excelente tutorial de JPA](http://www.davidmarco.es/blog/entrada.php?id=144)
- [Configuración de Derby para trabajar en memoria](http://wiki.apache.org/db-derby/InMemoryBackEndPrimer)
- [Configuración de JPA para usar Hibernate](http://eskatos.wordpress.com/2009/10/26/unit-test-jpa-entities-with-in-memory-derby)
- [Hibernate en entornos JavaSE](http://docs.jboss.org/hibernate/entitymanager/3.5/reference/en/html_single/#architecture-javase)
- [Comparativa de implementaciones de JPA](http://terrazadearavaca.blogspot.com/2008/12/jpa-implementations-comparison.html)
