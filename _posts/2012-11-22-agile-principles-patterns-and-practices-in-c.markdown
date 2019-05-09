---
title: "Agile principles, patterns and practices in C#"
date: 2012-11-22 11:22
author: Rubén Chavarría
categories: 
- Reseñas
- Agile
comments: true
published: true
footer: false
sidebar: true
---

##### Robert C. Martin

[![Agile principles, patterns and practices](http://vig-fp.prenhall.com/bigcovers/0131857258.jpg)][1]

## Por qué lo he leído

Lo he leido porque me he encontrado referencias a este libro en libros 
anteriores que he leído, en blogs sobre desarrollo de software que suelo leer 
y en otros muchos sitios relacionados con el software. Si encuentro tantas 
referencias, será por algo, ¿no? Además, el autor es muy conocido y valorado, 
así que no había excusa para no leerlo.

<!-- more -->

## Qué esperaba

Me esperaba un libro de <em>Uncle Bob™</em>. Ya he leído alguno del mismo 
autor, y me gusta su estilo. Algunas veces me parece un poco extremista, pero 
creo que es así porque cree en lo que hace y eso es lo que predica. Cuando 
creo que exagera, no le hago mucho caso y sigo hacia adelante, ya está.

Esperaba una descripción de las metodologías ágiles aplicadas al momento de 
escribir software y encontré ...

## Qué encontré

... un pedazo de ladrillo! Me asusté cuando vi la extensión del libro, pero 
enseguida entendí el porqué. El libro está lleno de diagramas 
<a href="http://es.wikipedia.org/wiki/Lenguaje_Unificado_de_Modelado">UML</a> 
y de código fuente (primero los tests, por supuesto). Así que es normal que 
sea tan largo.

En cuanto al contenido, me gustó mucho la descripción que hace de muchos 
patrones de diseño, (incluso he aprendido alguno que no conocía). En el libro 
también podrás encontrar una descripción detallada de los principios 
<a href="http://es.wikipedia.org/wiki/SOLID_(object-oriented_design)">SOLID</a> 
y de otros principios sobre cómo organizar y empaquetar los distintos 
componentes de tu aplicación (clases, paquetes, namespaces, lo que sea).

## Conclusiones

Aunque el libro sea muy extenso, me ha gustado por varias razones:

- He aprendido nuevos patrones de diseño
- He podido profundizar sobre el patrón Model-View-Controller (ver enlaces 
más abajo)
- He encontrado una descripción muy detallada de los principios 
<a href="http://es.wikipedia.org/wiki/SOLID_(object-oriented_design)">SOLID</a>

## Pasajes que quiero recordar de este libro

> Un módulo que es difícil de cambiar, está roto y necesita ser arreglado, 
aunque funcione

<!-- more -->

> Un módulo que no comunica está roto y necesita ser arreglado

<!-- more -->

> Cuanto más conocen los programadores sobre <em>todo</em> el proyecto, más 
sano y más informado está el equipo que lo desarrolla

<!-- more -->

> Es el <em>big picture</em> lo que mantiene unido el sistema. Es la visión 
del sistema lo que hace obvia la localización y la forma de los módulos 
individuales. Si la forma de un módulo es inconsistente con la <em>metáfora</em>, 
es el módulo quien está mal, no la metáfora

<!-- more -->

> Al final, el código fuente <em>es</em> el diseño

<!-- more -->

> Se sabe que el software se está pudriendo cuando empieza a mostrar alguno de 
los siguientes síntomas: rigidez, fragilidad, inmovilidad, viscosidad, 
complejidad innecesaria, repetición innecesaria u opacidad

<!-- more -->

> El elemento más volatil en los proyectos software son los requisitos. 
Vivimos en un mundo de requisitos cambiantes, y nuestro trabajo es estar 
seguros de que nuestros software puede sobrevivir a esos cambios, así que no 
culpes a los requisitos cambiantes por los fallos en el software

<!-- more -->

> Los principios SOLID: <strong>S</strong>ingle responsability principle, 
<strong>O</strong>pen close principle, <strong>L</strong>iskov substitution 
principle, <strong>I</strong>nterface segregation principle, 
<strong>D</strong>ependency inversion principle

<!-- more -->

> Un motivo de cambio es un motivo de cambio sólo cuando el cambio ocurre, 
mientras tanto no

<!-- more -->

> <em>Strategy </em>and <em>Template method</em> son las formas más comunes de 
satisfacer Open closed principle. Estos patrones representan una clara 
separación de la funcionalidad genérica de la implementación detallada de 
esa funcionalidad

<!-- more -->

> <em>Fool me once, shame on you. Fool me twice, shame on me.</em> Inicialmente, 
escribimos nuestro código pensando que no va a cambiar. Cuando ocurre un cambio, 
implementamos abstraciones que nos protegen de futuros cambios de esa misma 
naturaleza

<!-- more -->

> Liskov substitution principle nos lleva a una importante conclusión: un 
modelo, visto aisladamente, no puede ser validado significativamente. La 
validez de un modelo puede ser expresado solo en términos de sus clientes

<!-- more -->

> Liskov substitution principle clarifica que en la programación orientada a 
objetos, una relación de herencia pertenece al comportamiento que puede ser 
asumido y que los clientes dependen de este comportamiento, lo contrario de lo 
que normalmente se cree, que la herencia pertenece al estad

<!-- more -->

> El diseño de grandes sistemas depende críticamente de un buen diseño de 
componentes (paquetes, entregables, ...), de esta forma, los equipos 
individuales puede enfocarse en componentes aislados en lugar de preocuparse 
por el sistema completo

<!-- more -->

> Las interfaces pertenecen al cliente que las usa, no a la implementación. 
El enlace lógico entre el cliente y el interfaz es más fuerte que la relación 
entre el interfaz y sus implementaciones. Es tan fuerte que no tiene sentido
desplegar el cliente sin el interfaz, pero sí que lo tiene desplegar el 
interfaz sin sus implementaciones

## Otras lecturas y enlaces relacionadas

- [Agile principles, patterns and practices in C#][1] en Amazon
- [pdf] <a href="http://www.objectmentor.com/resources/articles/TheHumbleDialogBox.pdf">The humble dialog box</a>: 
cómo separar la lógica de negocio de la interfaz gráfica, de Michael Feathers.
- <a href="http://www.martinfowler.com/eaaDev/ModelViewPresenter.html">Patrón model-view-presenter</a>: 
artículo de Martin Fowler que me llevó a éste de 
<a href="http://www.martinfowler.com/eaaDev/uiArchs.html">Arquitecturas GUI</a>.
- <a href="http://apagayvuelveaencender.blogspot.com.es/2012/11/metodologias-agiles-me-las-creo-o-no-me.html">Metodologías ágiles: ¿me las creo o no me las creo?</a>: 
excelente post de <a href="http://twitter.com/andres_viedma">Andrés Viedma</a> 
que me viene ni al pelo como enlace relacionado con el libro y donde se explican 
los cuatro principios del desarrollo de software ágil
- Hace ya un tiempo, leí sobre
[principios y patrones de diseño]({{ site.baseurl }}{% post_url 2010-03-04-principios-y-patrones-de-diseno %}),

[1]: https://amzn.to/2HKRMKr
