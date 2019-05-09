---
title: "Mi primera aplicación web con AngularJS"
date: 2013-10-17 22:00
author: Rubén Chavarría
comments: true
categories: 
- JavaScript
- AngularJS
published: true
footer: false
sidebar: true
---

Esta semana no he podido aportar ningún tutorial a la serie de 
[demos de tecnologías JavaEE](/blog/2013/09/03/demos-tecnologias-javaee) ya
que he dedicado grandes esfuerzos a realizar una prueba técnica para una
empresa.

La prueba consitía en realizar una aplicación web, donde el back-end está
programado en PHP y el front-end en JavaScript, utilizando el framework MVC
[AngularJS](http://angularjs.org).

Ha sido una experiencia interesantísima. Ya tenía conocimientos de arquitecturas
MVC, he participado profesionalmente en multitud de desarrollos siguiendo
este modelo, pero ésta ha sido una oportunidad increíble de conocer un
framework tan de moda y tan demandado como AngularJS. El proyecto consistía en
implementar una [librería de videos de youtube](http://rct-ytlibrary.herokuapp.com).

<!-- more -->

![Puedes añadir un vídeo arrastrando y soltando]({{ site.baseurl }}/assets/images/2013/ytlibrary-dnd.png)

En definitiva, he aprovechado esta oportunidad, y con unas pequeñas modificaciones
a la prueba técnica inicial, he eliminado la necesidad de un back-end, he creado
un servidor web básico en *NodeJS*, y he desplegado la aplicación en *heroku*.

Si te pica la curiosidad y quieres ver el código fuente, lo puedes encontrar en mi 
repositorio de github [rchavarria/ytlibrary](http://github.com/rchavarria/ytlibrary).

La aplicación explota multitud de conceptos de AngularJS:

- Directivas más comunes: `ng-model`, `ng-repeat`, `ng-click`, ...
- Controladores, `angular.controller(...)`
- Servicios, implementados como factorías con `angular.factory(...)`
- Directivas, `angular.directive(...)`
- Posibilidad de arrastrar y soltar vídeos para añadirlos a la lista
- Animaciones con el módulo proporcionado por AngularJS `ngAnimate`

![Visualizar un vídeo desde la lista]({{ site.baseurl }}/assets/images/2013/ytlibrary-video.png)

Si todavía tienes ganas de más, te invito a que eches un vistazo a 
[Youtube library](http://rct-ytlibrary.herokuapp.com). Por supuesto, si quieres,
me encantaría que me contases qué te ha parecido.
