---
title: "Mis notas sobre Codemotion 2014"
date: 2014-11-29 00:48
author: Rubén Chavarría
comments: true
categories: 
- events
- codemotion
published: true
footer: false
sidebar: true
---

Por tercer año consecutivo asistí al evento Codemotion, "un evento de
desarrolladores para desarrolladores". Me encanta la descripcion del
evento. La verdad es que es una pasada, un evento al que este año acudimos
casi 2000 profesionales del desarrollo sofware, donde unos ponente (incluso
extranjeros) cuentan sus experiencias en la vida real. Impresionante.

Antes de nada me gustaría agradecer a los organizadores del evento, a todos
los voluntarios que nos soportan, a los patrocinadores y no me puedo olvidar
de la Universidad San Pablo CEU, que cedió las instalaciones.
Hay muchas quejas por *el intenné* sobre ciertos aspectos de la organización:
salas abarrotadas, comida insuficiente,... Creo que tienen razón, pero
también hay que entender que un evento así no es fácil organizarlo. A mí
me ha encantado la cantidad de tiempo disponible entre charla y charla. No
me he perdido ninguna de las charlas a las que quería asistir.

![Codemotion]({{ site.baseurl }}/assets/images/2014/codemotion.png)

<!-- more -->

Este año he podido disfrutar más de las charlas técnicas que el año pasado,
por lo que he aprendido y conocido multitud de nuevas herramientas,
técnicas e ideas.

Aún así, me he quedado con una espinita clavada. Me hubiera gustado
*pasillear* algo más, pero no se puede tener todo, o pasillo o charla.
También me hubiera gustado acercarme a más ponentes para darles las gracias
y comentar con ellos las tecnologías o herramientas que expusieron.

Pero no todo está perdido, he conocido a unos cuantos buenos profesionales
más y eso es una parte importante de estos eventos: ver viejos amigos y
hacer nuevos.
 
## Notas sobre las charlas

Y a continuación, una transcripción de algunas notas que fuí tomando en
todas las charlas a las que asistí. En la 
[agenda del Codemotion](2014.codemotion.es/es/agenda.html)
podrás encontrar cada una de las charlas que se impartieron con detalles
del ponente, presentaciones, vídeos,... Para ir aguantando hasta el año
que viene.

### What if everything is awesome, Christian Heilmann

Opinión de la charla: muy amena, se nota que Christian es un profesional dando
charlas por todo el mundo; muy buena historia, muy bien hilada y cortita, al
grano.

La prensa publicita casos demasiado idílicos.

Los programadores tenemos tendencia a recrear (reinventar la rueda) en lugar de
mejorar (¿porqué si no hay N variantes de frameworks web, por ejemplo?). **Mejora
las cosas que ya existen**

No expliques, demuéstralo con código o algo mejor, arregla el bug.

Si tus aplicaciones están dirigidas por datos, duraran mucho tiempo.

Agradece, da feedback, a tus usuarios y a los creadores de tus apps.

**Acción**: Echar un vistazo a los recursos de las diapositivas.

### Lean Node.js, Ricardo Borillo

Opinión: multitud de herramientas, multitud de consejos prácticos. De la charla
salí con alguna idea para poner en práctica inmediatamente.

Ricardo hace incapié en cuatro puntos lean:

1. eficiencia / automatización
2. no cometer errores
3. evitar desperdicios
4. mejora contínua

Relativo a la construcción de nuestra aplicación: 

- grung Vs gulp para automatización de tareas
- browser sync: inyecta CSS en el navegador sin recargar la página, para evitar
errores y conseguir un desarrollo más rápido.

Relativo a testear nuestra aplicación:

- Solo se puede reducir el numero de errores con tests.
- karma, jasmine, karma + virtual box (probar IE en Linux o Mac), protractor

Relativo al despliegue:

- upstart (reinicia servidor en caso de que caiga)
- forever (nodejitsu)
- fusion passenger, nginx + docker
- pm2 (cluster, monitorización, ...)

Código y ejemplos en el [repo Codemotion de R. Borillo](https://github.com/borillo/codemotion-2014)

### Workshop, designing a release pipeline, Jose Luis Soria

Opinión: el taller me defraudó un poco, porque al final fue más una charla larga
que un taller propiamente dicho. Aunque me llevé algunos consejos e ideas que me
pueden servir en mi día a día.

9 pasos a seguir para diseñar una pipeline de entrega:

1. Definir componentes: nombre, dependencias, deploy target, ...
2. Identificar subpipelines: 1 solo pipeline o 1 pipeline por componente o 1 pipeline por
equipo
3. Definir etapas y orquestación
a. cada etapa me tiene que dar feedback, información
b. crecer a lo ancho, no a lo largo (en el flujo, paralelizando etapas)
c. necesito: nombre, meta a conseguir, fuentes, flujo, ...
4. Definir entornos (no deben estar atados a etapas)
5. Definir los pasos (partes de cada una de las etapas)
6. Definir automatizacion y herramientas
7. Definir modelo ejecucion
8. Planificar para futuras mejoras: comienza simple y evoluciona
9. Inspecciona y adáptate (mejora contínua)

Recursos:

- libro Continuous Delivery
- Agile testing cuadrant
- Herramientas de orquestación: ThoughtWorks Go, MS VS Release Management

### Loves always takes care and humility, Chema Alonso

Opinión: la charla comenzó muy bien, una bonita historia (aunque me perdí la
primera parte el año pasado), va contando conceptos de seguridad,... Hasta que
aparece en pantalla *LATCH*. A partir de ahí, todo pareció un anuncio, y mi
cerebro desconectó.

La charla cuenta una historia entre una Developar y un Hacker.

Dev: preocupada por la seguridad. Cree que algo está seguro si está bien hecho
(best practices).

Hacker: tiene muchas otras maneras de romper la seguirdad.

Hacker: quiere nuevos metodos aplicando la ciencia: doble factor autenticación, usb con llave,
matrices de numeros, ...

Dev: ve problemas, a cada nuevo método le encuentra una debilidad.

### 20 languages in 40 minutes, Alonso Torres

Opinión: charla muy amena y friki, una pasada. El tono fue muy tranquilizador y
Alonso transmitia confianza. En definitiva, me encantó.

¿programar es un arte? no lo sé, pero sí se que es creativo

Alonso nos quiere dar una razón para cada uno de los lenguajes, porque en charlas
técnicas de 1h intentan venderte de usar su lenguaje. Alotor le sobra con 2 min/lenguaje

OOP Vs Functional

- scala tiene ambos
- haskell
- F#
- clojure: lenguaje funcional con cierta flexibilidad

Estático Vs Dinámico

- groovy: ambos
- python: para aprender dinámico
- ruby: favorece implícito (potencia sin control)
- php: desarrollo rápido
- js: para integración con otros sistemas

De sistema, de bajo nivel

- C: potencia
- C++: añade cierta estructura a C
- Go: concurrencia
- Rust: gestión memoria

Lenguajes del sigle XXI

- ceylon: modularidad
- elm: funcional en interactivo (I/O): es un haskell para el navegador
- julia: cálculo científico y macros

Y para terminar, Piet: cada pixel, con su color, es una instruccion. El
hola mundo con este lenguaje es el más bonito que he visto nunca.

Las slides y los ejemplos de código en el [repo Codemotion de Alotor](https://github.com/Alotor/20-languages-demos)

### Keynote del segundo día

Presentación del producto IBM Bluemix, una especie de heroku, Google App Engine,...

- learn
- be fast
- avoid the grind

**Acción**: buscar presentacion para dar con los 3 consejos.

### Teaching programming online, Pamela Fox

Opinión: no venía muy convencido a la charla, pensaba que trataría de docencia, de
cómo enseñar a programar online. En lugar de eso Pamela destripó el curso que da
sobre ciencia de la programación: herramientas, problemas, diversas actividades, ...

Si quieres que la gente vea tus vídeos, haz que duren menos de 10min

Frameworks y herramientas: Backbone, FB React Vs Angular; js parsers, js hint, js babyhint,...

Si alguna vez creas un sistema de programación online, chequea los bucles infinitos.
Los tendrás que sufrir, seguro.

También, deberás tener herramientas, que mediante diferenciación, sea capaz de
detectar si dos alumnos han copiado. Estos cursos suelen tener miles de alumnos, y
es imposible detectarlas manualmente.

Actividades de las que consta el curso en Kahn Academy:

- Exercises
- Projects: permiten a los alumnos ser más creativos.
- Algoritmo de votado para crear una lista de los proyectos más llamativos, y cómo
los alumnos se las ingenian para engañar al sistema.
- Spin­offs: o una vuelta de tuerca más a los proyectos.

En definitiva:
aprende > practica > crea > comparte > ayuda

[Live editor](https://github.com/Khan/live-editor) es el proyecto en el que está
trabajando la ponente.

### Analizando y debuggeando tu plataforma, Luis Bosque

Opinión: esperaba algo diferente de la charla, no sé muy bien el qué, pero algo 
diferente. Con todo esto, estuvo muy bien. Multitud de herramientas, multitud de
consejos y muchos ejemplos reales usados en CartoDB.

No valen las sensaciones, debes analizar tu plataforma para saber cómo se comportan
tus usuarios y para saber cómo afectan los cambios que haces.

No hay un manual sobre que medir, pero no hay que medir todo.

Analisis corto plazo: monitoring, alerting.

Analisis medio plazo: buscar patrones de uso, optimizar para su uso. Análisis de casos
especiales te pueden llevar a optimizaciones a incorporar

Stadísticas al usuario:

- tiempo de sus queries en ejecutarse
- número de visualizaciones de su app
- widgets más usados

Herramientas análisis logs: logstash, fluentd, splunk, syslog

No volverte loco con las métricas, no se puede medir todo, debes decidir qué 
precisión quieres (queries de mas de 30seg), definir una politica de retención de
datos (no todas las métricas tienen el mismo ciclo de vida)

Ante todo, ten en cuenta el impacto técnico, es muy, muy grande.

### Lo que la cafeína le hizo a JavaScript, Sergio Arbeo

Opinión: charla muy divertida y amena, Sergio comunica muy bien y se nota que sabe
de lo que habla. La charla es muy técnica y va de cosas muy sencillas hasta
ciertos problemas que te hacen estrujarte la mente un poco.

CoffeeScript mejor que ES5, CoffeeScript peor que ES6

¿Qué trae ES6?

- Destructuring, con su operación inversa, funciona con arrays
- Modules
- let / const
- classes
- propiedades computadas (ejemplo de código implementando `pluck`
- function: sspread operator: convierte varios argumentos en un array
- function: sdefault parameters
- arrow functions

**Acción**: Librería ESNext para usar ES6 hoy

### The Google Glass revolution, Alain Regnier, @altolabs, GDG Paris

Opinión: impresionante por la demo en vivo de las gafas. Me sirvió para
conocer de primera mano las Google Glass y pasar un poco de envidia de
poder cacharrear con un prototipo tecnológico.

- Multitud de sensores
- Organizado en Cards: como si fuera un timeline
- Controles: voz, táctil, mover cabeza
- Glass Mobile, MyGlass web
- Un detalle queno me gustó nada es que parece muy enlazado a tu móvil

Programar para GGlass

1. Mirror API: nunca te conectas a tu GGlass
tu server ­> google server ­> tus gafas
2. GDK: accede a hardware de tu GGlass
3. WearScript: javascript para wearables

### Usando behat para no abusar de F5, Alfonso Machado, GeeksHub

Opinión: una charla muy práctica, donde Alfonso nos cuenta su experiencia con `behat` a raiz
de unos problemas que tuvo él. Ejemplos con código y demo en vivo. Muy interesante.

Implementación de Gerkin inspirado en Cucumber

Mink: drivers para emular navegadores con Selenium (java and the like) + acciones predefinidas

Instalacion difícil, mejor con composer

### Scrum bad smells, Juanma Gómez

Opinión: muy animada, Juanma conecta perfectamente con la gente. Intentó tirar de nosotros,
pero era la última hora y nos resistíamos un poco. Eso sí, a la hora de las preguntas la
gente se extendió bastante. Buena señal.

Patrones en la implantación agile

- 2 trampas: yo ya lo se todo; esto no se puede hacer
- Las empresas esperan que no cambien nada
- “nosotros hacemos nuestro scrum”
- equipo multidisciplinar no es que todos hacemos de todo, no es un hombre orquesta, sino que es
un equipo con perfiles especializados que se complementan
- dueño de producto sin capacidad (o experiencia) en la toma de decisiones o de visión estratégica
- jefe de proyecto que pasa a scrum master: el rol del SM es complejo porque debe tratar
sobretodo de personas
- Iteraciones variables
- Definir todo al principio (como en cascada)
- Hacer cascadas pequeñas
- Control y seguimiento en lugar de responsabilidad y confianza
- “yo ya he hecho mi trabajo”

Mitos:

- ser agil es ser rápido
- en scrum sólo hay visión a corto plazo: debemos tener una visión a largo plazo

Como resumen:

- 1º aprender
- siempre hay alcantarillas que abrir, siempre va a salir algo que huele mal
- scrum conlleva un cambio cultural
