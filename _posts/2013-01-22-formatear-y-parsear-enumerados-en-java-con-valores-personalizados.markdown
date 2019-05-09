---
title: "Formatear y parsear enumerados en Java con valores personalizados"
date: 2013-01-22 13:17
author: Rubén Chavarría
comments: true
categories: 
- java
- programming
- enum
published: true
footer: false
sidebar: true
---

A partir de la versión 1.5 de Java, nos encontramos con un tipo de datos, un tipo 
especial de clases podríamos decir, los enumerados. Los tipos enumerados sirven para
acotar los posibles valores que puede tomar una variable o tipo de objeto. Java 
proporciona un método para transformar un enumerado en cadena, `name()`, y un método 
estático para convertir una cadena en uno de los valores del enumerado, 
`valueOf(String)`. Pero estos métodos son un poco limitados, ya que no nos permiten
personalizar los valores a los cuales son transformados los enumerados.

<!-- more -->

Partiremos del siguiente código describiendo tres valores en un enumerado:

```java
public enum States {
  EVERYTHING_IS_OK,
  SOMETHING_WENT_WRONG,
  TOTAL_FAILURE;
}
``` 

Así, sin más, podemos obtener la representación en `String` de `States.TOTAL_FAILURE` 
simplemente llamando al método `States.TOTAL_FAILURE.name()`. De la misma forma, usando
la llamada `States.valueOf("EVERYTHING_IS_OK")` es fácil imaginar qué valor del enumerado
obtendremos.

Pero, y si en lugar de esa representación a `String`, ¿queremos definir la nuestra 
propia?. Por ejemplo, siguiendo la siguiente tabla:

- EVERYTHING_IS_OK &rarr; green
- SOMETHING_WENT_WRONG &rarr; yellow
- TOTAL_FAILURE &rarr; red

## Formatear a cadena

Formatear es sencillo, y directo. Podemos declarar un campo `value` donde almacenar el
valor al cual queremos transformar el enumerado, y podemos sobreescribir el método
`toString()` de la siguiente manera:

```java
public enum States {
  EVERYTHING_IS_OK("green"),
  SOMETHING_WENT_WRONG("yellow"),
  TOTAL_FAILURE("red");

  private String value;

  private States(String value) {
    this.value = value;
  }

  public String toString() {
    return value;
  }
}
```

## Parsear desde una cadena

El problema viene cuando queremos obtener un valor del enumerado a partir de un `String`.
Supongamos que la transformación la vamos a hacer en un método estático, que por contraste
con el anterior método llamaremos `fromString`. Veamos qué opciones tenemos, de menos a 
más apropiadas:

### Sentencias if

La primera solución que le viene a uno a la cabeza es usar sentencias `if`. 

```java
[...]
public static States fromString(String fromValue) {
  if("green".equals(fromValue)) {
    return EVERYTHING_IS_OK;
  } else if("yellow".equals(fromValue)) {
    return SOMETHING_WENT_WRONG;
  } else if("red".equals(fromValue)) {
    return TOTAL_FAILURE;
  }
  throw new IllegalArgumentException("Wrong value: " + fromValue);
}
[...]
```

No hay mucho que decir aquí, simplemente que se debería evitar a toda costa esta solución.

### Bucle for

Otra solución, un poco más elegante, pero básicamente siguiendo la misma filosofía, podría
ser utilizar un bucle para recorrer los posibles valores del enumerado:

```java
[...]
public static States fromString(String fromValue) {
  for(States state : values()) {
    if(state.value.equals(fromValue)) {
      return state;
    }
  }
  throw new IllegalArgumentException("Wrong value: " + fromValue);
}
[...]
```

Esta solución es un poquito mejor, ya que si modificamos los valores posibles del enumerado, 
no es necesario que modifiquemos este método.

### Prealmacenamiento de los valores en un Map

Existe una solución que no involucra el uso de sentencias `if`, lo cual es muy positivo, ya
que estamos evitando la posibilidad de error, ya que no tendremos que formular una condición.

Esta solución la encontré en un hilo el de Stack Overflow [how can I lookup a Java enum 
from its string value?](http://stackoverflow.com/questions/1080904/how-can-i-lookup-a-java-enum-from-its-string-value).
Lo que pretende esta solución es crear una estructura de datos, y cuando se quiera transformar
un `String` en un valor del enumerado, simplemente se consulte esa estructura de datos.

La estructura de datos será un `Map` estático, que se rellenará en un bloque estático y 
consultaremos en nuestro método `fromString`.


```java
[...]
private static Map<String, States> dictionary;
static {
  dictionary = new HashMap<String, States>();
  for(States state : values()) {
    dictionary.put(state.value; state);
  }
}
[...]
public static States fromString(String fromValue) {
  States state = dictionary.get(fromValue);
  if(state == null) {
    throw new IllegalArgumentException("Wrong value: " + fromValue);
  }
  return state;
}
[...]
``` 

## Peligros de esta última solución

En Stack Overflow, un comentario a la respuesta donde encontré la solución sugiere que esta solución
puede causar problemas debido al classloader.

Pero he investigado un poco el tema, y parece que el comentario es erróneo, al menos para el
uso de los enumerados que estoy exponiendo aquí. Según el 
[ejemplo 8.9.2-1 de la especificación del java](http://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html#d5e12253),
primero se inicializan los valores del enumerado, luego la variable estática y finalmente
se ejecuta el bloque de código estático, estando ya todos los valores del enumerado 
inicializados.

Aquí os dejo unos cuantos enlaces a que confirman que la última solución es correcta:

- [Bootstrapping static fields within enums](http://blog.deepincode.com/2006/12/bootstrapping-static-fields-within-enums) y en enlace encontrado en ese mismo post: [Type Safe Enumerations in Java 5.0](http://blog.deepincode.com/2006/11/type-safe-enumerations-in-java-50) (buscar al final de este último post).
- Otro hilo de Stack Overflow, [When are these class and subclass static blocks executed (for an Enum)?](http://stackoverflow.com/questions/6827987/when-are-these-class-and-subclass-static-blocks-executed-for-an-enum) que me lleva al recurso definitivo: 
- [Java Language Specification - Example 8.9.2-1](http://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html#d5e12253): Si la documentación de Oracle sobre java es errónea, apaga y vámonos.

## Otras soluciones

Por supuesto que existen otras soluciones, quizá mejores que la última que propongo, pero
no he querido hacer más largo este post y he querido centrarme en proponer una alternativa
a los métodos `.name()` y `.valueOf()`, pertenecientes al propio enumerado.

Es por esto por lo que he descartado usar clases externas para formatear o parsear el 
enumerado, lo cual me habría hecho llegar a otras soluciones bien distintas. Pero si crees
que tu solución es muchísimo mejor que ésta, déjame un comentario, será bienvenido.
