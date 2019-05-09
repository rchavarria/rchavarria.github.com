---
title: "Madrid Software Crafters 2018"
date: 2018-03-06 21:34
author: Ruben Chavarria
comments: true
categories: 
- personal
- conferences
published: true
footer: false
sidebar: true
---

En este post dejo las notas que tomé en el Open Space 
[Madrid Software Crafters](http://madswcraft.com/). La verdad es que tenía 
ganas de que se celebrara un evento así por Madrid. La distancia y sobretodo 
la pereza, me pueden, y todavía no me he decidido a asistir a eventos 
similares que se celebran en Barcelona o Pamplona.

El día fue espectacular, no tanto por las charlas, pero sí por las personas 
con las que tuve el placer de compartir el día

![MadSWCraft]({{ site.baseurl }}/assets/images/2018/madswcraft.jpg)

<div style="text-align: center">
  <span style="font-size: 60%">
    <a href="https://twitter.com/madswcraft/status/967447494526488576">Imagen</a> reproducida con permiso de <a href="https://twitter.com/HelderDOliveira">Helder de Oliveira</a>, autor de la misma. Gracias!!
  </span>
</div>

<!-- more -->

Y ahí van las notas de cada sesión:

### Estrategias de *decoupling* en *legacy code*, con Rony Ancorini y Toño de la Torre

Primera estrategia, Interaction Driven Design. Simplificando, de una clase/fichero 
enorme, se extrae una parte (la que tenemos que modificar) a una clase/componente 
más pequeño y aprovechamos para testearlo.

Segunda, un poco bestia, un gran Feature Toggle (por tienda de ropa). Si está 
activado, en lugar de ejecutar el monolito (legacy), se ejecuta un sistema 
totalmente distinto (el nuevo, el *bonito*).

Su cliente entiende que el legacy hace mucho (ha ido creciendo orgánicamente, se 
ha ido añadiendo funcionalidades sin orden alguno) y que habrá que ir avanzando 
a muchas aplicaciones más pequeñas.

Pro tip: trabajar directamente con los usuarios del sistema, para ir teniendo 
feedback. El Feature Toggle va a ir tienda por tienda.

### Taller: Parallel changes, cambios grandes pasos pequeños, con Eduardo Ferro - [slides](http://www.eferro.net/2018/02/slides-taller-parallel-changes-software.html)

El título del taller parecía prometer, y el material necesario era bastante fácil 
de conseguir. Y la verdad es que la prometió.

La idea del taller es espectacular: se van proponiendo escenarios donde se parte 
de una situación inicial y hay que realizar un cambio para llegar a la situación 
objetivo. Dicho así es muy sencillo, pero hay una serie de reglas/restricciones 
que hay que cumplir (no se puede parar el servicio, los despliegues deben ser 
mínimos y cuanto más pequeños mejor,...).

Los escenarios propuestos van desde sencillos cambios de peticiones de un cliente 
a un servidor, hasta la interacción de varios servicios, pasando por consultas 
a bases de datos.

En el taller aprendí alguna estrategia a aplicar en migraciones de bases de datos 
y a prestar atención a los cambios que hacemos a nuestros sistemas, porque pueden 
tener más consecuencias de las que podemos pensar en un principio.

La idea fue aplicada a arquitecturas/sistemas/servicios, pero podría ser aplicada 
a refactorizaciones de código, gestión de la configuración,... Muchos otros campos.

### Effects, co-effects y subscriptions in SPAs, con Manuel Rivero - [slides](https://drive.google.com/file/d/1VtVziPtOvI68AQiMcq5nq2YGO1YI_x4D/view)

Podríamos definir *side-effect* como aquello que una función hace al *mundo* 
exterior. De la misma forma, podríamos definir *side-cause* como aquello que el 
mundo hace a mi función (datos que necesita mi función pero no es pasado como 
parámetro).

Así, un *effect* sería un *side-effect* y un *co-effect* sería un *side-cause*.

Para conseguir que mis funciones no dependan del mundo exterior, se podría aplicar 
un concepto que se parece mucho a inyección de dependencias, pero aplicado a 
funciones. La idea es que ahora, tus funciones reciben co-effects y devuelven 
effects. Del manejo de effects y co-effects se encarga el lenguaje o la librería 
en cuestión, dejando a tus funciones como funciones puras, fácilmente 
entendibles, fácilmente testeables.

Subscripciones de la librería [re-frame](https://github.com/Day8/re-frame) 
(librería ClojureScript con un concepto similar a React en JavaScript): funciones 
que hacen una query sobre el estado de la applicación y el resultado lo pasan 
a las funciones que renderizan la vista. Similar a las funciones de 
[ReactiveX]({{ site.baseurl }}{% post_url 2017-12-12-programacion-reactiva-javascript %}) que tenía 
funciones que podías ir encadenando.

Juraría que Manuel recomendó una charla, con un título parecido a 
*Arquitecturas front unidireccionales*, relacionada con Cycle.js, pero sólo 
soy capaz de encontrar el artículo 
[Unidirectional user interface architectures](https://staltz.com/unidirectional-user-interface-architectures.html) 
de André Staltz. No hay nada como preguntar, Manuel me pasó las slides y 
encontré el enlace a la charla: 
[Unidirectional data flow architectures](https://vimeo.com/168652278).

### Guarda tu ego en el cajón, con Alberto (aka APA42)

Bueno, a ésta llegué realmente tarde, y con un buen debate bastante avanzado, 
así que tampoco pude aprovercharlo tanto como me hubiera gustado. Aún así, 
me quedo con dos cosas:

1. Si quieres hacer que alguien cambie, tienes que darle una motivación para 
que la otra persona quiera cambiar
2. Ha ocasiones en las que las razones técnicas NO valen, así que para esas 
ocasiones, no intentes convencer a la otra persona con razones técnicas, si 
no con razones económicas, personales,...

## ¿Qué me llevo?

Parece que no atendí a muchas charlas, y así es. Bueno, el taller abarcaba 
varias charlas, así que esa es una de las razones. Otra es que tampoco surgieron 
charlas que me atrajeran demasiado, pero eso es problema mío. Pero la mejor 
excusa para no haber asistido a charlas es que disfruté mucho de las conversaiones 
en los pasillos conociendo a mucha gente nueva.

## ¿Qué tengo que mirar?

- Interaction Driven Design, de Sandro Mancuso
- PSR7 y PSR15, ¿de qué van? ¿cuántos PSRs hay?
- ¿Qué fuente usó Eduardo Ferro en las slides de su taller? 
[Sniglet](https://fonts.google.com/specimen/Sniglet)
- En las slides de Manuel Rivero hay un enlace a una app para aprender 
gramática (spelling). ¿Interesante para Einar?
- Relacionada con Cycle.js, charla 
[Unidirectional data flow architectures](https://vimeo.com/168652278)
- Método Suzuki, para comunicarse, convencer al otro, psicología,...
- [The core protocols: a guide to greatness](https://www.amazon.es/Core-Protocols-Guide-Greatness/dp/0692381082), 
de Richard Kasperowski

## Referencias

- [Notas sobre el Open Space](https://github.com/SoftwareCraftersMadrid/resumen-madswcraft18) 
en el GitHub de SW Crafters Madrid
- [Slides del taller sobre Parallel Changes](http://www.eferro.net/2018/02/slides-taller-parallel-changes-software.html), 
de Eduardo Ferro
- [Slides sobre la charla de effects y co-effects](https://drive.google.com/file/d/1VtVziPtOvI68AQiMcq5nq2YGO1YI_x4D/view), 
de Manuel Rivero

## Personas

Todos estos eventos van de personas, de ver a compañeros de profesión, 
viejos (o no tan viejos) amigos, y de crear nuevas relaciones. Ahí van 
unas cuantas personas con las que me encontré (perdón, no me acuerdo de 
todas), sin ningún orden en particular: 
[Manuel Rivero](https://twitter.com/trikitrok), 
[Ronny Ancorini](https://twitter.com/RonnyAncorini), 
[Toño de la Torre](https://twitter.com/adelatorrefoss), 
[Eduardo Ferro](https://twitter.com/eferro), 
[Modesto San Juan](https://twitter.com/msanjuan), 
[Abel](https://twitter.com/amisai), 
[Jesús](https://twitter.com/jeslopcru), 
[Rubén](https://twitter.com/rubendm23), 
[Juan David](https://twitter.com/juandvegarguez), 
[Alberto](https://twitter.com/APA42), 
[Raúl Villares](https://twitter.com/RaulVillaresBg), 
[Helder de Oliveira](https://twitter.com/HelderDOliveira),... 
(arg, maldita memoria)
