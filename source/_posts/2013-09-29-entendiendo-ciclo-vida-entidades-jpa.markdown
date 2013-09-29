---
layout: post
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
[tutoriales de demostración de tecnologías J2EE](/blog/2013/09/03/demos-tecnologias-javaee) y 
en esta en particular aprenderemos los estados del ciclo de vida de una entidad
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

Antes de nada, existen unas entidades y unos test sencillos, de ejercitación y puesta a
punto de JPA, Hibernate (implementación de JPA para esta demo) y Derby (el motor de
base de datos utilizada aquí). 

Echa un vistazo primero a estas clases (`Person`, `ContactablePerson`, `Phone`) y a los
tests (`BasicPersistenceTest` y `AdvancedPersistenceTest`) para poder comprender mejor
el ciclo de vida que describiremos a continuación.

## Estados de una entidad JPA

## Ciclo de vida, transiciones

## Ejecución

`mnv test`.

## Enlaces para ampliar información

