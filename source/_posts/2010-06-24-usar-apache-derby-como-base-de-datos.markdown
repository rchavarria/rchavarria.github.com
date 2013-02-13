---
layout: page
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

En este post vamos a aprender a usar <a href="http://db.apache.org/derby/">Apache Derby</a> como base de datos para nuestra aplicación Java. Seguiremos paso por paso un ejemplo de uso muy sencillo.

<!-- more -->

<h2>Instalación</h2>
Lo primero que deberemos hacer es descargar la última versión de Apache Derby: <a href="http://db.apache.org/derby/derby_downloads.html">página de descarga</a>. La descarga recomendada sería la distribución binaria, que incluye las librerías, documentación y herramientas de ayuda.

Acto seguido descomprimimos la distribución a un directorio de nuestra elección, por ejemplo:
<pre>C:\Archivos de programa\Java\derby-10.6
</pre>
Para poder usar derby, deberemos configurar nuestro entorno, es decir, deberemos establecer ciertas variables de entorno con los valores adecuados para poder ejecutar derby en nuestro PC. Suponiendo que vamos a usar Windows como sistema operativo, deberemos establecer las siguientes variables de entorno:
<pre>set DERBY_HOME=C:\Archivos de programa\Java\derby-10.6
set PATH=%DERBY_HOME%\bin;%PATH%
</pre>
De esta forma conseguiremos tener accesibles los ejecutables de las herramientas proporcionadas por derby.

A partir de ahora, para poder utilizar derby en nuestros programas Java, sólo será necesario tener accesible la librería <em>derby.jar</em> en el classpath de nuestro programa.
<h2>Código de ejemplo</h2>
De acuerdo, ya sabemos lo que tenemos que hacer para poder usar derby. Pero, ¿cómo lo usamos?. A continuación vamos a estudiar varios fragmentos de código que nos permitirán crear una base de datos, crear una sencilla tabla en nuestra base de datos, insertar datos y realizar consultas. Para ello se presupone un conocimiento básico de lenguaje SQL. Si quieres aprender un poco más sobre él puedes aprender un poco en <a href="http://www.w3schools.com/sql/">SQL Tutorial de W3C</a>.
<h3>Crear una base de datos</h3>

{% codeblock Crear una base de datos programáticamente %}

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

{% endcodeblock %}

Para ejecutar scripts SQL y realizar otras consultas, derby proporciona la herramienta <em>ij</em>, el uso de la cual lo podemos aprender de la siguiente guía: <a href="http://db.apache.org/derby/docs/10.6/getstart/">getting started with derby 10.6 (inglés)</a>.
Como el nombre de la base de datos es <em>/DerbyDB/ExampleDB</em>, la base de datos será creada en el directorio
<pre>C:\DerbyDB\ExampleDB</pre>
<h3>Insertar datos</h3>
Con el siguiente código seremos capaces de introducir datos en nuestra tabla:

{% codeblock Insertar datos %}

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

{% endcodeblock %}

<h3>Realizar consultas</h3>
Con el siguiente código, realizamos una consulta a nuestra tabla y mostramos por consola la información en ella almacenada:

{% codeblock Realizar consultas %}

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

{% endcodeblock %}


Espero que este post os sirva para poder utilizar derby como base de datos.
<div id="_mcePaste" style="overflow:hidden;position:absolute;left:-10000px;top:1232px;width:1px;height:1px;"><!--[if gte mso 9]&gt;  Normal 0 21   false false false        MicrosoftInternetExplorer4  &lt;![endif]--><!--[if gte mso 9]&gt;   &lt;![endif]--><!--  /* Style Definitions */  p.MsoNormal, li.MsoNormal, div.MsoNormal  {mso-style-parent:"";   margin:0cm;   margin-bottom:.0001pt;  mso-pagination:widow-orphan;  font-size:12.0pt;   font-family:"Times New Roman";  mso-fareast-font-family:"Times New Roman";} a:link, span.MsoHyperlink   {color:blue;  text-decoration:underline;  text-underline:single;} a:visited, span.MsoHyperlinkFollowed  {color:purple;  text-decoration:underline;  text-underline:single;} @page Section1  {size:612.0pt 792.0pt;  margin:70.85pt 3.0cm 70.85pt 3.0cm;   mso-header-margin:36.0pt;   mso-footer-margin:36.0pt;   mso-paper-source:0;} div.Section1   {page:Section1;} --><!--[if gte mso 10]&gt; &lt;!   /* Style Definitions */  table.MsoNormalTable   {mso-style-name:&quot;Tabla normal&quot;;   mso-tstyle-rowband-size:0;  mso-tstyle-colband-size:0;  mso-style-noshow:yes;   mso-style-parent:&quot;&quot;;  mso-padding-alt:0cm 5.4pt 0cm 5.4pt;  mso-para-margin:0cm;  mso-para-margin-bottom:.0001pt;   mso-pagination:widow-orphan;  font-size:10.0pt;   font-family:&quot;Times New Roman&quot;;  mso-ansi-language:#0400;  mso-fareast-language:#0400;   mso-bidi-language:#0400;} --> <!--[endif]-->
<p class="MsoNormal">Para ejecutar scripts sql y realizar otras consultas contra una bbdd derby, existe la herramienta ij. El uso de esta herramienta lo podemos aprender de la siguiente guía: <a href="http://db.apache.org/derby/docs/10.6/getstart/">getting started with derby 10.6 (ingles)</a>.</p>

</div>