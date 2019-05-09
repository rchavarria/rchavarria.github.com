---
title: "Global day of code retreat 2017"
date: 2017-11-22 21:52
author: Ruben Chavarria
comments: true
categories: 
- software craftsmanship
- events
published: true
footer: false
sidebar: true
---

Al igual que el [año pasado], he tenido el placer de participar en el Global
Day of Code Retreat 2017, un evento sobre programación *de intensa práctica,
enfocado en los fundamentos del diseño y desarrollo de software*. Este año ha
habido 136 eventos repartidos por todo el mundo. No he encontrado estadísticas
sobre cuantas personas participamos, pero estoy seguro de que con tantos
eventos tuvimos que ser miles.

¿Impresiona eh? ¿Te animarás el año que viene? El funcionamiento es sencillo:
se trata de resolver el problema del [juego de la vida de Conway], donde unas
*células* viven o mueren de acuerdo a una serie de reglas preestablecidas.
Siempre se programa por parejas (o tríos), nunca solo. El día está dividido en
iteraciones de una duración determinada, y al final de cada iteración hacemos
una pequeña retrospectiva. Y así es como fue nuestro [día].

![GDCR 2017]({{ site.baseurl }}/assets/images/2017/gdcr2017.jpg)

<div style="text-align: center">
  <span style="font-size: 60%">
Imagen propiedad de <a href="https://twitter.com/HelderDOliveira">Helder</a>, reproducida con su permiso
  </span>
</div>

<!-- more -->

## El día

Cada iteración duró unos 45 minutos. Según va avanzando el día, va aumentando
la intensidad de las conversaciones. Y también el cansancio. Para poner un poco
de emoción al asunto, en cada nueva iteración se pueden proponer una serie de
restricciones. Además, las restricciones de una iteración se acumulaban para la
siguiente. Por ejemplo, en la segunda iteración, debíamos programar haciendo
[ping-pong] *(uno escribe el test, otro lo hace pasar y escribe un nuevo test,
otro lo hac...)*. Más adelante se propuso eliminar los `else` y más adelante
todos los condicionales.

Después de cada iteración, se hace una pequeña retrospectiva, donde todos
ponemos en común cómo hemos afrontado el problema, qué impedimentos hemos
encontrado, cómo lo hemos solucionado, hasta dónde hemos llegado. En seguida
aparecieron 2 enfoques principales para atacar al problema:

1. De dentro hacia afuera: se comienza a resolver el problema por la parte más
   interna, más pequeña, más acotada. Se empiezan a describir las reglas del
   juego en los tests y se van haciendo pasar, implementando las reglas en una
   función o en pequeños objectos con muy poco código.
2. De fuera hacia adentro: el problema se ataca desde el nivel más alto. Se
   suele hablar de *mundo*, *universo*, *juego*, *matriz de células*. Las
   reglas del juego se implementan mucho más adelante. Pero al principio te
   encuentras con problemas como recorrer una matriz, bucles anidados,
   inicialización del juego, comprobación de límites,...

Durante las retros suele haber alguna discusión/conversación. En esta ocasión,
especialmente en la última, hubo una interesante discusión que surgió a raiz de
restricciones relacionadas con no usar ni condicionales ni bucles. Sobre los
condicionales no hubo mucha dicrepancia, parece que tenemos claro que una forma
de reemplazar condicionales es el polimorfismo (aplicarlo ya es otra historia),
aunque no es la única.

Pero sobre los bucles no hubo mucho consenso. ¿Realmente eliminarlos ayuda a
hacer el código más legible? ¿Ayuda a tener menos código (y por tanto menos
probabilidad de errores)? Si el código no queda muy legible, ¿estoy tratando a
mis compañeros como inferiores? ¿o les estoy ayudando a aprender
características del lenguaje? Una pregunta que surgió varias veces: ¿Un
`map`/`filter` es un bucle?

El formato ofrece cierta libertad. Por ejemplo, las iteraciones no tienen
porqué durar 30 minutos exactos. Nosotros, como novedad, y como ahorro de
energía (parece mentira, pero es bastante agotador), en la última iteración
hicimos [mob programming]. Y, todo sea dicho, es la iteración que menos
avanzamos. El cansancio y las restricciones acumuladas hacían mella en
nosotros. Había que tener en cuenta más de dos puntos de vista, ya no era
programar en parejas.

Es curioso, este año he sentido que he avanzado más en la solución al problema
que en otras ocasiones. No estoy seguro, mirándolo con perspectiva, es como si
este año hubiera estado más centrado en el software y no tanto en las personas.
Puede que haya sido porque he afrontado el evento con más tranquilidad, al
pensar/saber que allí encontraría a algún conocido.

## La gente

Aunque sienta que he estado más centrado en el software que en la gente, este
tipo de eventos tratan sobre la profesión y los profesionales. Por eso me
gustaría recordar que allí me volví a encontrar con gente como [Juan David],
[Helder] y [Luis], organizadores y facilitadores del evento. 

Me reencontré con [Alberto], o bueno, más bien él me reencontró a mí, al
principio no le reconocí, y juraría que ya nos habíamos visto anteriormente.

Casualidades de la vida, conocí a un alcalaíno, [Abel]. Y como buen habitante
de la vega del Henares, espero verle mucho por [Codenares], la comunidad de
desarrollo del... Henares, sí.

También tuve reencuentros de hace muchísimo tiempo, de [mi primer GDCR], del
cual guardo un grato recuerdo, donde conocí a [Rafa].

Y algún otro que no pude quedarme con una forma de contactar con ellos, como
Enrique, pero que seguro que nos volveremos a ver en un *fregao* de estos.

## Agradecimientos

Por supuesto a [idealista], por facilitar las instalaciones y la comida... y
gente, que estuvieron allí para que los demás pudieramos disfrutar. Y también,
cómo no, a los facilitadores/organizadores Juan David, Helder y Luis.

¡Gracias!

## Referencias

- Libro sobre el [Juego de la vida]
- Repositorio de [Software Crafter Madrid] sobre el evento y [algunas fotos]
nada comprometedoras

[año pasado]: {{ site.baseurl }}{% post_url 2016-10-27-global-day-of-code-retreat-2016 %}
[juego de la vida de Conway]: https://es.wikipedia.org/wiki/Juego_de_la_vida
[día]: https://github.com/SoftwareCraftersMadrid/global-day-of-coderetreat-2017/blob/master/theday.md
[ping-pong]: http://wiki.c2.com/?PairProgrammingPingPongPattern
[mob programming]: https://en.wikipedia.org/wiki/Mob_programming
[Juan David]: http://juandavidvega.es/
[Helder]: https://twitter.com/HelderDOliveira
[Luis]: http://twitter.com/luisrovirosa
[Alberto]: https://twitter.com/APA42
[Abel]: https://twitter.com/amisai
[Codenares]: https://twitter.com/codenares
[mi primer GDCR]: {{ site.baseurl }}{% post_url 2014-11-18-mi-primer-code-retreat %}
[Rafa]: https://twitter.com/rafael_luque
[idealista]: http://idealista.com
[Juego de la vida]: https://leanpub.com/4rulesofsimpledesign
[Software Crafter Madrid]: https://github.com/SoftwareCraftersMadrid/global-day-of-coderetreat-2017
[algunas fotos]: https://www.meetup.com/es-ES/madswcraft/photos/28339208/
