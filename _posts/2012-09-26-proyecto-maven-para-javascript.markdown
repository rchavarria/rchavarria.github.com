---
title: "Proyecto maven para javascript"
date: 2012-09-26 09:26
author: Rubén Chavarría
categories: 
- software
- JavaScript
- programming workout
comments: true
published: true
footer: false
sidebar: true
---

Estoy aprendiendo JavaScript. Creo que es uno de los lenguajes con más futuro, 
y no sólo por la web (que da de comer a mucha gente), sino por herramientas como 
[PhoneGap](http://phonegap.com/) (que te permite crear aplicaciones para iOS, 
Android, ...), y también por la llegada del nuevo Windows 8, ya que se pueden 
desarrollar aplicaciones en JavaScript que acceden al hardware de la máquina 
donde esté instalado Windows 8.

Empecé aprendiéndolo gracias a 
[Codecademy](http://www.codecademy.com/), que comenzó el año con unos cursos o 
clases online, y me llamó mucho la atención la posibilidad de poder ir 
practicando JavaScript sin tener que instalar nada. Y además, cada semana la 
herramienta me recordaría que tenía una nueva lección, así no dejaría de 
practicar.

<!-- more -->

Pero hace poco tropecé con un pequeño problema, y es que quería aportar una 
solución escrita en JavaScript al desafío de 
[Compresión en RLE](http://www.solveet.com/exercises/Compresion-RLE/35) en 
[Solveet](http://www.solveet.com/) (una plataforma donde la gente publica 
desafíos de programación y otra gente publica sus propias soluciones, muy 
recomendable y divertido). El problema era que no tenía instalado nada en mi 
ordenador que me permitiera hacer 
[TDD](http://es.wikipedia.org/wiki/Desarrollo_guiado_por_pruebas) (lo prefiero 
para resolver los desafíos, así practico doble: el desafío y la práctica TDD).

Una herramienta que me encanta para gestionar el ciclo de vida de mis 
proyectos es [maven](http://maven.apache.org), así que me decidí a buscar 
algo que me permitiera escribir JavaScript y luego ejecutarlo con comandos 
de maven.

Y tuve la suerte de encontrar un post de 
[akquinet](http://blog.akquinet.de/) donde explica 
[cómo crear un proyecto maven para JavaScript](http://blog.akquinet.de/2011/02/11/mavenizing-javascript-projects/).
La verdad es que es realmente sencillo porque akquinet se ha currado un 
archetype para maven que te crea un esqueleto de proyecto para que escribas 
directamente JavaScript. Simplemente con este comando para ejecutar maven:

```bash
mvn archetype:generate \ 
  -DarchetypeArtifactId=javascript-quickstart \ 
  -DarchetypeGroupId=de.akquinet.javascript.archetypes \ 
  -DarchetypeVersion=1.0.0 \ 
  -DgroupId=<enter your groupId> \ 
  -DartifactId=<enter your artifactId>
```

Con el proyecto creado a partir del archetype de akquinet podrás:

- Ejecutar tus tests JavaScript con 
[Jasmine](http://pivotal.github.com/jasmine/)
- Comprimir los ficheros `.js` y `.css` de tu proyecto
- Generar la documentación con 
[JSLint](http://www.jslint.com/) y 
[JSDoc](http://code.google.com/p/jsdoc-toolkit/)

Además, al ser un proyecto maven, es muy fácil que lo integres en un servidor de
[Integración Contínua](http://es.wikipedia.org/wiki/Integraci%C3%B3n_continua) 
como [Hudson](http://hudson.dev.java.net/).

Si quieres, puedes ver la solución que aporté en Solveet. El desafío es muy 
sencillo, y hay muy poco código JavaScript: 
[Compresión RLE en JavaScript](http://www.solveet.com/exercises/Compresion-RLE/35/solution-846),
el 
[código completo con los tests](https://github.com/rchavarria/solveet-problems/tree/master/rle-compression-javascript).
