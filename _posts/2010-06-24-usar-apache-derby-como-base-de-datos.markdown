---
title: "Usar apache derby como base de datos"
date: 2010-06-24 09:44
author: Rubén Chavarría
comments: true
categories: 
- derby
- apache
- base de datos
published: true
footer: false
sidebar: true
---

<div style="margin:2%; padding:2%; background-color:#E0E0E0; ">
  <p>Este post pertenece a mi antiguo blog en <a href="http://rchavarria.wordpress.com">wordpress</a>, pero decidí pasarme a github:pages por las siguientes <a href="/blog/2012/12/03/por-que-cambie-mi-blog-en-wordpress-com">razones</a></p>
</div>

En este post vamos a aprender a usar [Apache Derby](http://db.apache.org/derby/) como base 
de datos para nuestra aplicación Java. Seguiremos paso por paso un ejemplo de uso muy 
sencillo.

<!-- more -->

## Instalación

Lo primero que deberemos hacer es descargar la última versión de Apache Derby: 
[página de descarga](http://db.apache.org/derby/derby_downloads.html).
La descarga recomendada sería la distribución binaria, que incluye las librerías, 
documentación y herramientas de ayuda.

Acto seguido descomprimimos la distribución a un directorio de nuestra elección, por 
ejemplo: `C:\Archivos de programa\Java\derby-10.6`

Para poder usar derby, deberemos configurar nuestro entorno, es decir, deberemos 
establecer ciertas variables de entorno con los valores adecuados para poder ejecutar 
derby en nuestro PC. Suponiendo que vamos a usar Windows como sistema operativo, 
deberemos establecer las siguientes variables de entorno:

```
set DERBY_HOME=C:\Archivos de programa\Java\derby-10.6
set PATH=%DERBY_HOME%\bin;%PATH%
```

De esta forma conseguiremos tener accesibles los ejecutables de las herramientas 
proporcionadas por derby.

A partir de ahora, para poder utilizar derby en nuestros programas Java, sólo será 
necesario tener accesible la librería `derby.jar` en el classpath de nuestro programa.

## Código de ejemplo

De acuerdo, ya sabemos lo que tenemos que hacer para poder usar derby. Pero, 
¿cómo lo usamos?. A continuación vamos a estudiar varios fragmentos de código que nos 
permitirán crear una base de datos, crear una sencilla tabla en nuestra base de datos, 
insertar datos y realizar consultas. Para ello se presupone un conocimiento básico de 
lenguaje SQL. Si quieres aprender un poco más sobre él puedes aprender un poco en 
[SQL Tutorial de W3C](http://www.w3schools.com/sql/).

### Crear una base de datos

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

public class CreateDataBase {

  public static void main(String[] args) {
    String driver = &quot;org.apache.derby.jdbc.EmbeddedDriver&quot;;
    String dbName = &quot;/DerbyDB/ExampleDB&quot;;
    String dbParam = &quot;create=true&quot;; //la base de datos se creará si no existe todavía
    String connectionURL = &quot;jdbc:derby:&quot; + dbName + &quot;;&quot; + dbParam;
    Connection conn = null;

    try{
      Class.forName(driver);
    } catch(java.lang.ClassNotFoundException e) {
      e.printStackTrace();
    }

    try {
      conn = DriverManager.getConnection(connectionURL);

      Statement st = conn.createStatement();
      String sqlCreateTableUsers =
             &quot;CREATE TABLE users ( &quot; +
             &quot;FirstName VARCHAR(20) NOT NULL, &quot; +
             &quot;LastName VARCHAR(20) NOT NULL, &quot; +
             &quot;idUser INTEGER NOT NULL CONSTRAINT idUser_PK PRIMARY KEY &quot; +
             &quot;)&quot;;
      // la sentencia SQL crea una tabla con 3 campos
      st.execute(sqlCreateTableUsers);

      System.out.println(&quot;La base de datos '&quot; + dbName + &quot;' se ha creado correctamente&quot;);
    }  catch (Throwable e)  {
      System.out.println(&quot;Error al crear la base de datos '&quot; + dbName + &quot;'&quot;);
      e.printStackTrace();
    } finally {
      try { conn.close(); }
      catch (Throwable t){}
    }
  }
}
```

Para ejecutar scripts SQL y realizar otras consultas, derby proporciona la herramienta 
`ij`, el uso de la cual lo podemos aprender de la siguiente guía: 
[getting started with derby 10.6 (inglés)](http://db.apache.org/derby/docs/10.6/getstart/).
Como el nombre de la base de datos es `/DerbyDB/ExampleDB`, la base de datos será creada 
en el directorio: `C:\DerbyDB\ExampleDB`

### Insertar datos

Con el siguiente código seremos capaces de introducir datos en nuestra tabla:

```java
String driver = &quot;org.apache.derby.jdbc.EmbeddedDriver&quot;;
String dbName = &quot;/DerbyDB/ExampleDB&quot;;
String connectionURL = &quot;jdbc:derby:&quot; + dbName;
Connection conn = null;

try{
  Class.forName(driver);
} catch(java.lang.ClassNotFoundException e) {
  e.printStackTrace();
}

try {
  conn = DriverManager.getConnection(connectionURL);

  Statement st = conn.createStatement();
  st.executeUpdate(&quot;INSERT INTO users VALUES('Jose', 'Olmedo', 1)&quot;);
  st.executeUpdate(&quot;INSERT INTO users VALUES('Maria', 'Hoz', 2)&quot;);

  System.out.println(&quot;Se han insertado dos registros&quot;);
} catch (Throwable e)  {
  System.out.println(&quot;Ha fallado la insercion de dos registros&quot;);
  e.printStackTrace();
} finally {
  try { conn.close(); }
  catch (Throwable t){}
}
```

### Realizar consultas

Con el siguiente código, realizamos una consulta a nuestra tabla y mostramos por consola 
la información en ella almacenada:

```java
String driver = &quot;org.apache.derby.jdbc.EmbeddedDriver&quot;;
String dbName = &quot;/DerbyDB/ExampleDB&quot;;
String connectionURL = &quot;jdbc:derby:&quot; + dbName;
Connection conn = null;

try{
  Class.forName(driver);
} catch(java.lang.ClassNotFoundException e) {
  e.printStackTrace();
}

try {
  conn = DriverManager.getConnection(connectionURL);

  Statement st = conn.createStatement();
  ResultSet rs=st.executeQuery(&quot;SELECT * FROM users&quot;);
  while (rs.next()){
    Integer idUser = rs.getInt(&quot;idUser&quot;);
    String first = rs.getString(&quot;FirstName&quot;);
    String last = rs.getString(&quot;LastName&quot;);
    System.out.println(idUser + &quot; se llama: &quot; + first + &quot; &quot; + last);
  }
  rs.close();
} catch (Throwable e)  {
  System.out.println(&quot;Ha fallado la consulta de datos&quot;);
  e.printStackTrace();
} finally {
  try { conn.close(); }
  catch (Throwable t){}
}
```

Espero que este post os sirva para poder utilizar derby como base de datos.

Para ejecutar scripts SQL y realizar otras consultas contra una bbdd derby, existe la 
herramienta `ij`. El uso de esta herramienta lo podemos aprender de la siguiente guía:
[getting started with derby 10.6 (ingles)](http://db.apache.org/derby/docs/10.6/getstart/)
