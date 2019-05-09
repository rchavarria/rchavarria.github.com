---
layout: post
title: "WeCodeFest 2019"
date: 2019-02-25 21:12
author: Ruben Chavarria
categories: 
- Eventos
---

El año pasado ya me quedé con las ganas de asistir al [WeCodeFest]. Mucha gente
a la que respeto por el trabajo que hacen, hablaba muy bien de una conferencia
nueva, en Valladolid. Bueno, no era tanto como una conferencia, era un evento 
más enfocado en la práctica, en arremangarse y probar cosas, hacer cosas. Y eso 
me gusta bastante, pero no pudo ser.

Este año sí, y ha sido super especial, me ha encantado. Se puede decir que es
un evento *pequeño*, organizado con mucho amor y mucho atención al detalle, y
sobretodo práctico. Lo más interesante no son las charlas programadas, si no
los talleres o las conversaciones planteadas en el open space.

![WeCodeFest 2019]({{ site.baseurl }}/assets/images/2019/wecode.jpg)

<!-- more -->

## Talleres

¿He dicho ya que lo más interesante eran los talleres? Aquí están aquellos
a los que asistí:

#### Introducción a Property Based Testing

Taller sobre testing automático impartido por [Sergio Arroyo Cuevas].
[Property Based Testing] se basa en ejecutar varias veces un mismo test,
usando datos aleatorios como entrada a nuestro código. De esta forma, trata
de encontrar casos límites (números muy grandes, o negativos, cadenas con un
formato peculiar,...) donde nuestro código puede fallar.

El taller estuvo muy bien organizado, en bloques fijos de tiempo, para
asegurar cierto avance a los asistentes. Comenzó suave, tomando contacto con
las librerías, y terminó probando código ajeno al taller, para demostrar lo
fácil/complicado que sería usar este tipo de testing en nuestro día a día.

Se podían utilizar distintos lenguajes, yo usé JavaScript. Puedes encontrar
las instrucciones y enlaces a cada uno de los lenguajes disponibles en el
repositorio [WeCodeProperties] de Sergio.

#### Programación cuántica para gente que programa

Taller impartido por [Salvador de la Puente] sobre un tema bastante desconocido
para mí, programar ordenadores cuánticos. Según trató de explicarnos Salva,
*no se trata de ordenadores más rápidos, sino de una forma de operar 
esencialmente distinta*.

El taller fue muy, muy práctico, y pudimos aprender los principales fenómenos 
de la computación cuántica tales como superposición, entrelazamiento e
interferencia. Lo de comprenderlos 100% lo dejé para otro día. No es que sean
conceptos complicadísimos de comprender, pero sí que son conceptos que uno
necesita reposar un tiempo.

Aún así, jugar con el simulador [Quirk] e implementar algunos algoritmos
cuánticos (puertas lógicas o pequeños cálculos) fue muy divertido. Esta es
la [presentación] que acompañó al taller.

También me sirvió para repasar conceptos básicos de computación, como lógica
booleana o las clásicas puertas lógicas.

#### Aplicación serverless en 2 horas

Taller impartido por [Vicenç García-Altés] donde el objetivo era desarollar
una aplicación para una universidad con servicios de AWS, donde la lógica
de negocio estuviera implementada a través de *Functions*/*Lambdas* en AWS.

El taller está basado en el repositorio [taller serverless] de Vicenç. En
él, hay mucho contenido, repito, **mucho** contenido. Se nota que hay un
inmenso trabajo detrás del taller. Se nota porque hay que integrar muchos
servicios y el taller está enfocado en tests, despliegues automáticos y otras
buenas prácticas que no suelen estar presentes en otros talleres.

En realidad, es un taller bastante más extenso de horas, de hecho, Vicenç
acaba de hacer público el taller [The Serverless Course], por si te quieres
apuntar.

## Open Spaces

En el open space salieron unas cuantas charlas/conversaciones interesantes. No
pude ir a todas las que me interesaban, aquí están las notas de las que sí fui:

#### Testing en front-end

No recuerdo quién la propuso.

Empezamos hablando sobre los distintos tipos de tests, y la conversación se
enfocó sobretodo en los tests end-to-end, donde todos coincidíamos en que son
los más costosos de escribir y ejecutar.

Luego, la conversación se dirigió hacia los equipos de QA, donde salió la idea
de que no debería haber equipos de QA separados de Desarrollo.

#### Desarrollo de software en provincias

Propuesta por [Azahara Fernández], aquí llegué un poquito tarde.

Se habló de coste en tiempo y energía personal que tienen los largos trayectos
de casa al trabajo y del trabajo a casa en las grandes ciudades, y del
ahorro en tiempo que hay al trabajar en ciudades más pequeñitas, donde puedes
estar en el trabajo en 15 minutos o menos.

También se habló de lo difícil que es, para las empresas tecnológicas, encontrar
talento en ciudades modestas. Luego, la conversación giró hacia la creación
de empresas, y se expuso que en el caso de Salamanca podemos encontrar varios
casos de pequeñas empresas cosiguiendo grandes cosas.

Esto me alegró bastante, trabajo en los alrededores de Madrid, pero me gusta
vivir en un lugar tranquilo, no en una gran ciudad, y saber que hay casos de
empresas en pequeñas ciudades que hacen cosas muy interesantes enciende un
rayo de esperanza en que algún día pueda trabajar para alguna de ellas.

También se habló de teletrabajo, y de cómo cada vez más los trabajadores
*exigimos* esa posibilidad. ¡Bien por nosotros!

#### Chatbot

Propuesta por Javier Rodrigo. En principio estaba pensado como taller, pero
para ello tendríamos que haber descargado una imagen de una máquina virtual
de unos pocos Gb. No muy práctico para hacerlo el día del evento.

Aún así, Javier salió del paso y nos lo enseñó en vivo y en directo. Incluso
nos enseñó toda la domótica que se ha instalado él mismo en su casa.

Compartió con nosotros el repo [HomeBot]
con la imagen y las instrucciones para comenzar a jugar con Node-Red, una
aplicación que nos permitirá crear un bot para Telegram en dos patadas.

Javier controla todo en su casa con [Home Asistant] y un hardware que usa
mucho son unos cacharritos llamados [sonoff] que puede controlar a través de
WiFi (se pueden buscar en Aliexpress).

#### Programación para niños

Propuesta por [Carlos Rueda] (enlace a [sus notas]).

Aquí hubo conversaciones muy entretenidas para padres y madres. Estos pequeños
nuestros nos traen de cabeza. Hubo un pequeño debate sobre si nuestros hijos
e hijas deberían tener la misma profesión que nosotros, y alguien hizo una
muy buena pregunta para hacernos reflexionar: ¿por qué queremos enseñar a
programar a nuestras hijas? Que cada uno se responda.

A parte de anécdotas divertidas, salieron por ahí unos cuantos recursos
interesantes:

- [FIRST Lego League], una competición científica para niños y niñas
- [Portal], un videojuego muy interesante
- [Box Island], juego infantil donde debes programar a tu personaje de una
forma parecida a Scratch
- [Arte generativo], repositorio de [Karlos G. Liberal] usado en un taller del
evento

#### Jueces online, programar por diversión

Lo siento, no me quedé con quién la propuso.

La gran mayoría de los asistentes eran alumnos de la Universidad de
Valladolid, y parecían bastante intersados en el tema. De hecho, unos de los
jueces de los que se habló fue precisamente uno de la propia universidad.

Me pareció muy curioso, que incluso uno de estos jueces tenga patrocinadores
o sponsors, que llegan a pagar los primeros posicionados dentro de algunas 
liga "privadas".

Una pega que le gente ve en este tipo de plataformas es el poco enfoque a la
calidad del código que se presenta, primando más la velocidad a la que se
responde al desafío u otros aspectos. Pero por ahí apareció [Exercism], que
se centra justo en lo contrario, se centra en crear relaciones mentor -
alumno, para recibir feedback del código presentado y poder aprender con 
cada ejercicio.

Otros jueces de los que se habló:

- [The Advent of Code], parece ser el más conocido
- Coding game
- El propio [juez de la universidad]
- Hacker rank
- [Project Euler]
- Coding wars
- Coding contest
- Hash code 

## Charlas

Y finalmente las charlas, lo *no tan interesantes* del evento:

#### Implementando APIs en 2019

Charla impartida por [Jose Ramón Huerga], donde comenzó hablando de *DX*, o
Developer eXperience, por contraposición con UX. Sería como un *marketplace*
de APIs, donde conseguir que nuestras APIs les gusten a los desarrolladores,
las usen, creen aplicaciones con ellas y paguen por su uso.

Habló de nuevos protocolos y tecnologías, como GraphQL o [AsyncAPI].

AsyncAPI no es una comunicación petición/respuesta, como REST, si no que es
asíncrono (me imagino que los WebSockets quizá tengan algo que decir por
aquí, tampoco concretó mucho sobre esto).

Hizo una demo en vivo, sobre cómo montar una API con GraphQL que tire de
peticiones REST a varios APIs a través de un API Gateway. Lo montó todo sobre
AWS, así que hubo bastantes servicios en la nube involucrados.

Lo interesante de todo es que los clientes solo ven un API, el expuesto a
través de GraphQL, cuando en realidad pueden estar consumiendo varios de ellos
por detrás. La flexibilidad de GraphQL permite agregarlos, seleccionar 
ciertos campos,...

## Personas

Hasta aquí la parte técnica, pero si este evento fue para mí tan especial
fue sobre todo por la gente que allí me encontré.

Los primeros, los organizadores, gente muy maja, super cercana y muy muy
atentos a que todo saliera bien y fuera como la seda: [Javier],
[Alvaro], [Jorge], [Amalia] y Óscar (había más, pero ellos son los que yo
conocí).

También conocí/me presenté a bastante gente nueva (aunque de algunos ya me
sonaba la cara): [Azahara], [Cristina], [Nerea], [Juan Manuel], [Salva],
[Carlos], [Claudia], [Vicenç] y [Daniel] son sólo algunos de ellos.

Y por último, volver a encontrarme con buenos profesionales y mejores personas:
[Alberto], [Manuel], [Abel] y [APA] entre otros.

Muchas gracias, fue un auténtico placer compartir con todos estos dos días
tan intensos.

## La conferencia en sí

La verdad es que ha sido un evento que he disfrutado muchísmo. Quizá porque ha
sido lejos de donde vivo (y me la he tomado como vacaciones), porque me ha
acompañado mi familia, o no se qué. Pero ha sido la leche.

Los organizadores pedían feedback por todos los lados. Pero no caía en saco
roto. Durante los dos días vi algunos detalles que no estaban perfectos, pero
la organización recogió *quejas* de los asistentes y reaccionó frente a ellas,
subsanándolas. La verdad es que me quedé bastante impresionado. ¡Olé por ellos!

En cuanto al feedback, no me gusta darlo *en caliente*, porque me da la impresión
de que puede ser demasiado negativo o demasiado positivo, pero tengo que 
forzarme a darlo, porque si no se me pasa el arroz, como me ha pasado aquí.
Antes de que pudiera agradecer o quejarme de algo, la organización ya había
reaccionado.

Una dinámica que me sorprendió mucho fue el concurso organizado usando la
aplicación Kahoot. Hizo que el concurso fuera muy divertido. Me lo apunto
para utilizarlo en algún cumpleaños o reunión de amigos.

Como muestra del buen rollo que irradia la WeCode, se propuso crear una
lista de música colaborativa, música que sonó durante la fiesta de clausura:
[lista de música de la WeCode].

Y por último, no quiero acabar el post sin darle las gracias a los patrocinadores,
que hicieron más asequible la asistencia al evento a todos los asistentes e
hicieron posible un evento al que realmente merece la pena asistir.

**¡Gracias!** 

[Sergio Arroyo Cuevas]: https://twitter.com/@delr3ves
[Property Based Testing]: http://blog.jessitron.com/2013/04/property-based-testing-what-is-it.html
[WeCodeProperties]: https://github.com/delr3ves/WeCodeProperties
[Salvador de la Puente]: https://salvadelapuente.com/
[Quirk]: https://algassert.com/quirk
[presentación]: https://bit.ly/2SpbZKR
[Vicenç García-Altés]: https://twitter.com/vgaltes
[taller serverless]: https://github.com/vgaltes/WCF
[The Serverless Course]: https://theserverlesscourse.com/
[Azahara Fernández]: https://twitter.com/azahara_fergui
[HomeBot]: https://github.com/frodcab/HomeBot
[Home Asistant]: https://www.home-assistant.io/
[sonoff]: https://www.itead.cc/sonoff-wifi-wireless-switch.html
[Carlos Rueda]: https://twitter.com/carlrue
[sus notas]: https://github.com/crueda/WeCodeProgramacionNi-os/blob/master/programacion_ni%C3%B1os.md
[FIRST Lego League]: https://www.firstlegoleague.es/
[Portal]: https://www.gamespot.com/portal/
[Box Island]: https://boxisland.io/
[Arte generativo]: https://github.com/karlosgliberal/ArteGenerativo
[Karlos G. Liberal]: https://twitter.com/@patxangas
[Exercism]: http://exercism.io/
[The Advent of Code]: https://adventofcode.com/
[juez de la universidad]: https://uva.onlinejudge.org/
[Project Euler]: https://projecteuler.net/
[Jose Ramón Huerga]: https://twitter.com/jrhuerga
[AsyncAPI]: https://www.asyncapi.com/

[Javier]: https://twitter.com/nhpatt
[Alvaro]: https://twitter.com/aloaisa
[Jorge]: https://twitter.com/semurat
[Amalia]: https://twitter.com/amaliahern
[Azahara]: https://twitter.com/azahara_fergui
[Cristina]: https://twitter.com/cristinafsanz
[Nerea]: https://twitter.com/sailormerqury
[Juan Manuel]: https://twitter.com/juanshac
[Salva]: https://salvadelapuente.com/
[Carlos]: https://twitter.com/carlrue
[Claudia]: https://twitter.com/m4nd3lbr0t
[Vicenç]: https://twitter.com/vgaltes
[Daniel]: https://twitter.com/delineas
[Alberto]: https://twitter.com/jalbertopaz
[Manuel]: https://twitter.com/trikitrok
[Abel]: https://twitter.com/amisai
[APA]: https://twitter.com/APA42

[lista de música de la WeCode]: https://open.spotify.com/playlist/5LFLfet0LRTipeiO8Hw9zt?si=CFb0ySRVRhu5yUlTieI9og
