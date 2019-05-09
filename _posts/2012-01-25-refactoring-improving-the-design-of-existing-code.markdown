---
title: "Refactoring: improving the design of existing code"
date: 2012-01-25 01:25
author: Rubén Chavarría
categories: 
- Reseñas
- Diseño
comments: true
published: true
footer: false
sidebar: true
---

##### de Martin Fowler, Kent Beck, John Brant, William Opdyke, Don Roberts

## Por qué lo he leído

[![Refactoring: improving the design of existing code](https://images-eu.ssl-images-amazon.com/images/I/41odjJlPgHL.jpg)][1]

El título me pareció sugerente. Me gusta que el código que utilizo, el código 
que escribo o el código que leo, tenga muy buena apariencia, sea legible, 
sencillo y, por qué no, sea bonito.

No soporto ver clases mal identadas, o con nombres que no significan nada. Lo 
odio. Y siempre he pensado que refactorizar el código ayuda a conseguir todo 
esto.

<!-- more -->

## Qué esperaba

Evidentemente, según el título, esperaba un manual, una guía, sobre cómo 
refactorizar. Esperaba que el libro me enseñara a refactorizar, a mejorar las 
refactorizaciones que hago en mi día a día.

Teniendo a Martin Fowler como autor principal, esperaba una descripción de 
experiencias, una demostración de veteranía, de la que poder beneficiarme y 
aprovechar esa sabiduría para mejorar en mi trabajo.

## Qué encontré

Encontré un catálogo de acciones de refactorización. Muchas de las 
refactorizaciones descritas en el libro son sencillas, otras ya las practicaba 
sin conocerlas formalmente y otras estoy seguro de que me resultarán muy 
útiles de aquí en adelante.

## Conclusiones

El libro me ha resultado un poco denso, y a veces muy lento, incluso llegó un 
momento en el que estuve a punto de dejar de leer.

Cada acción de refactorizar está muy detallada. Esto hace que leerlo sea un 
poco aburrido, pero como referencia no tiene precio.

Como ya he dicho antes, muchas refactorizaciones ya las estaba realizando 
personalmente, pero ni las había categorizado, ni les había puesto nombre. 
Por esto mismo, no he encontrado muchas refactorizaciones desconocidas para mí, 
pero al mismo tiempo me ha permitido categorizar, catalogar, varias 
refactorizaciones que estaba realizando. De las refactorizaciones nuevas, 
tengo pensado escribir sobre alguna de ellas.

Sin duda, es un libro a tener en cuenta para cualquier desarrollador software, 
tanto como para su lectura como para tenerlo de referencia. Totalmente 
recomendado.

## Pasajes que quiero recordar de este libro

> El primer paso, es construir un conjunto sólido de tests para el código que 
se va a refactorizar

<!-- more -->

> En la mayoría de los casos, un método debería residir donde los datos que el 
método usa

<!-- more -->

> Para refactorizar, lo mejor es pasito a pasito, lo que lleva a cometer menos 
errores

<!-- more -->

> La lección más importante del ejemplo es el ritmo del refactor: test, cambio 
pequeño, test, cambio pequeño, test, ..

<!-- more -->

> ¿Por qué refactorizar? Mejora el diseño del software, hace el software más 
fácil de mantener, ayuda a encontrar errores, ayuda a programar más rápido

<!-- more -->

> ¿Cuándo no refactorizar? Cuando es necesario empezar desde cero, o cuando 
estás cerca de una entrega

<!-- more -->

> Cuando los testers encuentran un bug, hay que hacer dos cosas: arreglarlo y 
crear un test que te asegure de que el bug no volverá a aparecer

<!-- more -->

> El estilo que yo sigo es el de fijarme en todas las cosas que la clase puede 
hacer y pruebo cada una de ellas para todas las condiciones que pueden hacer 
que la clase falle. No es lo mismo que testear cada uno de los métodos 
públicos. Los tests deben de exponer cierto riesgo

<!-- more -->

> La repetición es la raiz de todos los males del software

<!-- more -->

> (Las sentencias de protección indican: esto es raro, haz algo y sal de aquí) 
La sentencia de protección o retorna de la función o lanza una excepción, 
nunca debería dejar seguir ejecutando el método

<!-- more -->

> A veces, se da por supuesto algo y se escribe un comentario. Es mejor hacer 
explícita lo asumido creando una sencia assert

<!-- more -->

> Mi experiencia me dice que conforme refactorizar se va convirtiendo en una 
rutina, deja de ser una sobrecarga y comienza a ser algo esencia

## Referencias

- [Refactoring: improving the design of existing code][1], segunda edición en
Amazon

[1]: https://amzn.to/2CO5Fna
