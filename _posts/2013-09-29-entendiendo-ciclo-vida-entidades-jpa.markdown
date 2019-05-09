---
title: "Entendiendo el ciclo de vida de entidades JPA"
date: 2013-09-29 15:24
comments: true
categories: 
- tutorials
- Java EE
- JPA
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
    Find an English version of this post directly in the <a href="https://github.com/rchavarria/javaee-6-demos/tree/master/jpa-entities">source code repository</a>.
</div>

En esta demo aprenderemos en qué estados puede encontrarse una entidad JPA,
y qué métodos proporciona el estándar para transicionar una entidad de un
estado a otro. 

Se puede ver el código fuente de la demostración en el directorio 
[`jpa-entities`](https://github.com/rchavarria/javaee-6-demos/tree/master/jpa-entities)
del repositorio de las demos en github.

<!-- more -->

## Demo

Esta demo pertenece a una serie de 
[tutoriales de demostración de tecnologías J2EE]({{ site.baseurl }}{% post_url 2013-09-03-demos-tecnologias-javaee %}) y 
y en esta en particular aprenderemos los estados del ciclo de vida de una entidad
JPA y cómo transicionar entre ellos.

Una frase leída en uno de los enlaces que aparecen al final del post dice (traducción
libre):

> Si, a la hora de modificar entidades, piensas en ellas como transiciones de estados en lugar
de ejecuciones de sentencias SQL, harás tu desarrollo mucho más sencillo.

Y es que alguna ventaja tendría que tener lo que proporciona JPA, que es la abstracción
de la base de datos. Si no dejamos de pensar en SQL, nunca podremos abstraernos de la 
base de datos. Parece muy buena idea lo de ver la vida de una entidad como una serie
de transiciones de un estado a otro.

## Antes de comenzar

Antes de nada, existen unas entidades y unos tests sencillos, de ejercitación y puesta a
punto de JPA, Hibernate (implementación de JPA para esta demo) y Derby (el motor de
base de datos utilizada aquí). 

Echa un vistazo primero a estas clases (`Person`, `ContactablePerson`, `Phone`) y a los
tests (`BasicPersistenceTest` y `AdvancedPersistenceTest`) para poder comprender mejor
el ciclo de vida que describiremos a continuación.

## Estados de una entidad JPA

Una entidad se puede encontrar en alguno de estos estados:

- No existe todavía: no es un estado en sí, pero podría verse con el origen de todo.
- **Nueva**: la entidad se acaba de instaciar con el operador `new`, como una clase Java
de toda la vida. No está asociado a ningún contexto de persistencia.
- **Gestionada**: tiene una identidad persistente y está asociada a un contexto de
persistencia.
- **Separada**: tiene una identidad persistente pero no está asociada a un contexto de
persistencia.
- **Eliminada**: tiene una identidad persistente, está asociada a un contexto de persistencia,
pero está marcada para ser eliminada de la base de datos.

## Ciclo de vida, transiciones

En el siguiente diagrama, de la documentación de Oracle, se pueden ver las transiciones 
posibles de una manera gráfica.

![Transiciones de una entidad JPA](http://docs.oracle.com/cd/E16439_01/doc.1013/e13981/img/lifeent30.gif)

### Transición de nueva a gestionada

Fácilmente, con el método `persist`:

```java
@Test
public void testFromNewToManaged() {
    ContactablePerson p = createContactablePerson();

    em.persist(p);
    assertTrue("entity's state is 'managed'", em.contains(p));
}
```

### Transición de gestionada a separada

Existen dos formas:

1. Mediante el método `detach`.
2. Cerrando el gestor de entidades, `EntityManager.close()`.

Usando el método `detach`:

```java
@Test
public void testFromManagedToDetachedUsingDetachMethod() {
    ContactablePerson p = createContactablePerson();
    em.persist(p);

    em.detach(p);
    assertFalse("entity is not in persistence context", em.contains(p));
}
```

Cerrando el gestor:

```java
@Test
public void testFromManagedToDetachedClosingEntityManager() {
    ContactablePerson p = createContactablePerson();
    em.persist(p);

    tx.commit();
    em.close();
    
    try {
        em.contains(p);
        fail("em should be closed, and the entity shouldn't be managed by him");
    } catch (IllegalStateException e) { }
}
```

### Transición de separada a gestionada

```java
@Test
public void testFromDetachedToManaged() {
    ContactablePerson p = createContactablePerson();
    em.persist(p);
    em.detach(p);
    
    ContactablePerson mergedPerson = em.merge(p);
    
    assertFalse("original entity is not managed...", em.contains(p));
    assertTrue("... but merged one is", em.contains(mergedPerson));
}
```

Una entidad previamente gestionada pero que fue separada, es posible actualizarla
a un nuevo contexto de persistencia. Pero hay que tener cuidado, el objeto original
no es el que pasa a ser gestionado, si no que es el devuelto por el método `merge`.

### Transición de gestionada a eliminada

```java
@Test
public void testFromManagedToRemoved() {
    ContactablePerson p = createContactablePerson();
    em.persist(p);

    em.remove(p);
    assertFalse("entity has been removed and it is not managed", em.contains(p));
}
```

### Transición de eliminada a gestionada

Aunqe esta transición no está documentada en el diagrama anterior de Oracle, es posible
transicionar una entidad a gestionada una vez ésta ya ha sido marcada como eliminada. 
Dejo a elección del lector encontrarle utilidad y sentido a esta transición, ya que
aunque sea posible, dudo de su valor. Esta transición es posible si usamos el método
`persist` sobre la entidad eliminada.

```java
@Test
public void testFromRemovedToManaged() {
    ContactablePerson p = createContactablePerson();
    em.persist(p);
    em.remove(p);
    assertFalse("entity has been removed", em.contains(p));
    
    em.persist(p);
    assertTrue("entity is managed again", em.contains(p));
}
```

## Notas finales

Antes de terminar, me gustaría recalcar algo acerca de la creación del `EntityManagerFactory` 
y `EntityManager`, ya que es una cuestión muy importante a la hora de desarrollar nuestras
aplicaciones.

La creación de un `EntityManagerFactory` es **muy** costoso, y sólo se debería crear 
**una** vez en toda la vida de nuestra aplicación. Es por esta razón, que su creación
está en un método estático, que se ejecuta antes que cualquier test, y que sólo se 
ejecuta una vez para todos los tests de la suite:

```java
@BeforeClass
public static void classSetUp() {
    emf = Persistence.createEntityManagerFactory("test-jpa");
}
```

Por otro lado, la creación de una `EntityManager` es mucho más ligero, y la recomendación
dada por la documentación es la de crear una de ellas por cada transacción que vayamos
a realizar. Pero cuidado, esto no quiere decir que debamos crear una de ellas en
cada consulta a la base de datos, si no más bien, una por cada petición de la aplicación
cliente, es decir, que es una buena práctica agrupar varias consultas siempre y
cuando estas consultas tengan el objetivo de crear un único resultado al cliente.

Por esta razón de que es poco costoso crear un `EntityManager`, su creación se
realiza en el método `setUp` del test, de forma que tendremos un contexto de persistencia
limpio en la ejecución de cada uno de nuestros tests, pero reaprovecharemos las
conexiones a la base de datos, ya que éstas se mantienen en el `EntityManagerFactory`.

```java
@Before
public void setUp() throws Exception {
    em = emf.createEntityManager();
    // ...
}
```

## Ejecución

Esta demo se puede ejecutar como un test de JUnit, y estaría integrado en la ejecución
de `maven`, así que simplemente ejecuta el comando `mvn test` para ver los resultados.

## Enlaces para ampliar información

- [Código de la demo en github](https://github.com/rchavarria/javaee-6-demos/tree/master/jpa-entities)
- [Usar JPA, Hibernate y Derby](/blog/2011/05/19/uso-de-jpa-hibernate-y-derby):
un post en este mismo blog sobre cómo usar JPA, Hibernate como implementación del estándar
y Derby como base de datos.
- [An excellent JPA tutorial](http://www.davidmarco.es/blog/entrada.php?id=144): 
uno de los mejores tutoriales sobre JPA que he encontrado en español.
- [Hibernate EntityManager](http://docs.jboss.org/hibernate/core/4.0/hem/en-US/html_single): 
implementación de JPA dentro del framework Hibernate.
- [What is a JPA entity?](http://docs.oracle.com/cd/E16439_01/doc.1013/e13981/undejbs003.htm): 
documentación de Oracle sobre entidades JPA. 
- [Working with JPA entities objects](http://www.objectdb.com/java/jpa/persistence/managed): 
más documentación sobre entidades JPA.
