---
title: "Charla sobre eXtreme Programming"
date: 2014-09-20 01:27
author: Rubén Chavarría
comments: true
categories: 
- talks
- xp
- agile
published: true
footer: false
sidebar: true
---

![Prácticas de eXtreme Programming]({{ site.baseurl }}/assets/images/2014/xppractices.jpg)

Recientemente he dado una charla en el trabajo acerca de [eXtreme Programming].
No es nada del otro mundo, tampoco pretendo dar lecciones a nadie y tampoco
he descubierto nada que no estuviera escrito ya. Pero al hacer la charla he
reunido un poco de información de aquí y de allá, y ya que he hecho ese
pequeño esfuerzo, ¿por qué no plasmarlo aquí?

A continuación os dejo el guión que escribí mientras la preparaba. No conté
todo lo que está, ni está todo lo que conté, pero este fue mi pequeño trabajo
de campo.

<!-- more -->

## Introducción al desarrollo ágil de software

El desarrollo de software comenzó siendo hecho por ingenieros, de los de toda
la vida (que no quiere decir que sea malo, pero como veremos fue diferente),
lo que condicionó su forma de hacerlo, pero construir software es más parecido 
a crear una obra de arte: requiere *creatividad* y *artesanía*.

A diferencia de otros productos de la ingeniería, el software es maleable, 
muchas veces ilógico y siempre se encuentra incompleto (por eso se parece 
a una obra de arte).

Al entender estas diferencias es cuando empiezan a surgir nuevas forma de 
desarrollar software, como el desarrollo ágil de software.

No existen metodologías o procesos ágiles (en contra de todo lo que se vende 
últimamente), sólo existen **equipos ágiles**. Eso que se describe como 
metodología ágil no es más que la construcción de un entorno para que los 
equipos aprendan a ser ágiles.

Diferencias con lo que se venía haciendo hasta ahora:

- La forma en la que el equipo trabaja junto es más importante que cualquier 
proceso (gente y comunicación frente a procesos y herramientas).
- El cliente, el usuario, pasa a ser un miembro esencial del equipo.
- El mayor problema con el desarrollo de software son los requisitos 
cambiantes. Para la mayoría de los proyectos, aceptar los cambios puede 
costar menos que asegurar que los requisitos no van a cambiar nunca.

Al cambiar la forma de ver los cambios, resulta que es más fácil cambiar cómo 
se gestionan los proyectos. En lugar de gestionar actividades y esperar al 
final del todo a tener una aplicación, los agilistas gestionan los requisitos 
(aceptando que éstos van a cambiar) y se muestra al cliente cómo la aplicación 
va cambiando con el tiempo.

## Gestión por funcionalidades

En la gestión tradicional, se planifican las actividades una detrás de otra, 
cuando finaliza una comienza la siguiente. Así hasta el final del proyecto. 
Es entonces la única vez donde se muestra el software creado.

¿Cómo funciona? Los requisitos son constantes a lo largo del tiempo, y fluyen a 
través de las actividades como por una línea de montaje. Cada actividad finaliza 
con los requisitos a la vez  y al final de la línea se entrega un software. 
Podemos tener gente especializada en cada actividad, e ir cambiando de equipo 
según vamos cambiando de actividad. La única pega que tiene es que los requisitos 
no son constantes, por lo que todo lo demás no sirve de nada.

¿Y Agile? Agile considera que los requisitos no son constantes. Cada requisito, 
cada funcionalidad se presenta al cliente como una Historia de Usuario. El gráfico 
anterior se gira 90º y el proceso en sí mismo es el que permanece constante. Se 
planifican los requisitos por prioridad, y se va trabajando uno a uno pasándolo por 
todas las actividades, por lo que vamos teniendo requisitos completos poco a poco. 
Tener los requisitos priorizados permite cambiarlos a antojo. Y no solo eso, 
también permite finalizar el proyecto en el momento en el que queramos.

Este giro de 90º permite a los managers a tener una estimación de coste por 
requisito, no por actividad.

Uno de los costes de gestionar requisitos es que siempre hay que estar listo para 
nuevas funcionalidades, por lo que se debe mantener una calidad muy alta tanto en 
diseño como en código.

## Cómo evoluciona el software

En todo desarrollo de software llega un momento en el al que arreglar un bug, 
resulta que se crean uno o varios pequeños bugs por ahí dispersos.

Barry Boehm ya encontró que según va avanzando un proyecto software en su ciclo 
de vida, el coste de un cambio se vuelve cada vez más y más grande. Un concepto 
que lo explica mejor podría ser el Principio de Oxidación del Software.

Esta curva se comenzó interpretando de forma que se debían crear documentos de 
requisitos lo más detallados y lo más estáticos posibles. Agile no lo considera 
así, en lugar de eso se prepara para que los cambios en los requisitos cuesten 
poco.

Para eso, y para combatir la oxidación del software, Agile propone:

- Refactorizar: hacerlo sin descanso, sin límites, sin parar, sin excusas… 
refactoriza
- Tests: unitarios y de aceptación. También se aceptan otros: de integración, 
de sistema, de lo que sea, pero tests. Automáticos, eso si. Con ellos se logra 
eliminar el miedo a los cambios.
- Entrega temprana y frecuente: con ello se aumenta el feedback del cliente y 
ayuda a identificar cambios. Y cuanto antes se detecten estos cambios, menor 
coste tendrán.

¿Cómo mantener la capacidad de poder realizar cambios manteniendo el coste en 
niveles aceptables? Sólo porque el cliente no vea el código no significa que 
no tengamos que hacer esfuerzo para mantener la capacidad de realizar cambios. 
Y esto se consigue manteniendo un alto nivel de calidad, una baja complejidad 
y una cobertura de tests lo más alta posible.

## Introducción a XP

El primer proyecto en el que se usó eXtreme Programming comenzó el 6 de marzo 
de 1996. XP es uno de los famosos Procesos Ágiles, entre los que se encuentran 
Scrum, Kanban,…

En lugar de entregar todo lo que el cliente desea en un futuro lejano, XP va 
entregando el software trocito a trocito, según se va necesitando.

XP hace hincapié en el trabajo en equipo. Managers, clientes y programadores 
forman parte del mismo equipo. Los clientes se sienten bien siendo parte del 
equipo, los programadores contribuyen activamente y los managers se encargan 
de que exista una buena comunicación.

¿Por qué extremo? Por una serie de reglas y prácticas las lleva a su máxima 
expresión, mucho más que en proyectos tradicionales.

## De vuelta a lo básico, qué es lo que en realidad importa

Como ya sabemos, crear software es muy complicado. Por lo que no tiene sentido 
perder el tiempo en tareas que no importan. XP se deshace de tareas o actividades 
que se consideran que no aportan valor.

XP tiene una serie de reglas que se pueden englobar en estos cuatro aspectos:

- *Escuchar*: hay que aprender, hay que conocer el problema. Eso te dirá qué es 
lo que debes testear. Como probablemente no lo averigües tú solo, deberás 
escuchar a los clientes, a los usuarios, managers y demás gente de negocio.
- *Diseñar*: hay que escuchar lo que el código nos cuenta acerca de cómo quiere 
estar estructurado, y darle forma poco a poco.
- *Codificar*: si al final del día no hay un software ejecutable, no habrás 
hecho nada.
- *Testear*: hay que saber cuándo hemos terminado. De otra forma, estarás atascado 
pensando si todo cumple con lo establecido o no. Pero lo peor de todo, es que 
tampoco vas a saber cómo de cerca estás de tu destino.

## Reglas

Algunas reglas sueltas quizá no tengan sentido, pero combinadas se puede ver 
hacia dónde van, qué es lo que quieren conseguir.

### Escuchar

Se escriben Historias de Usuario (las cuales son el corazón de la planificación 
en un proyecto XP).

El proyecto se divide en iteraciones o sprints.

Al final de cada iteración, se realiza una pequeña entrega de funcionalidades.

Se crean tres niveles de planificación:

- Release plan: mira hacia el futuro unos cuantos meses y agrupa historias 
en grandes entregas.
- Next Iteration plan: se agrupan las historias que se van a realizar en 
la próxima iteración.
- Current Iteration plan: las historias definidas para esta iteración se 
dividen hasta que se encuentran tareas que se pueden acometer fácilmente.
Los planes se toman como algo vivo, no como algo estático. Si el cliente 
cambia de idea, se cambian los planes. Si el equipo se retrasa en una entrega, 
se cambian los planes.

Se intenta conseguir un Ritmo Sostenible.

Cada dia comienza con un Stand-up Meeting.

Se mide la Velocidad del Proyecto.

Se favorecen los Espacios Abiertos y se fomenta la Movilidad de las Personas.

### Diseñar

Simplicidad, se busca siempre lo más sencillo posible. Para poder mostrárselo 
al cliente lo antes posible y obtener feedback.

Siempre se usa una Metáfora del Sistema, se busca usar el lenguaje propio 
del negocio, la jerga que se usa en el entorno para el cual se está 
desarrollando el software.

Se crean Spikes, para reducir riesgos.

Ninguna funcionalidad se añade prematuramente (yagni).

Se Refactoriza en cualquier momento y en cualquier lugar que sea posible.

Se usan Tarjetas CRC para las decisiones de diseño. Así, todos los miembros 
del equipo entienden y contribuyen al diseño.

### Codificar

El cliente siempre está disponible para resolver dudas sobre el software.

El código se escribe siguiendo unos Estándares consensuados por el equipo.

Primero, se escriben los Tests Unitarios, luego el código de producción.

Todo el código de producción se escribe mientras se Programa por Parejas.

Se Integra Frecuentemente, mejor con Integración Contínua.

El código es de todos, Collective Ownership.

### Testear

En un proyecto XP, los programadores toman la actitud de ser ellos quien 
demuestran al cliente que los requisitos funcionan, y no al revés, no es 
el cliente quien demuestra que lo que pidió no funciona.

Todo el código debe tener Tests Unitarios. Y todos los tests pasan antes 
de sacar una versión.

Cuando se encuentra un bug, se crea un test para reproducirlo, arreglarlo, 
y que nunca vuelva a salir una versión con ese bug.

Se escriben Tests de Aceptación. Se ejecutan frecuentemente y su puntuación 
se hace pública.

## Valores

XP mejora un proyecto software en cinco aspectos fundamentales, que se han 
convertido en los valores de XP. Las reglas que acabamos de ver son consecuencia 
de maximizar estos valores.

- Simplicidad: se hace lo que es necesario, pero nada más. No se añade complejidad 
extra porque sí. Se avanza a pasos pequeños pero firmes.
- Comunicación: todo el mundo es parte del equipo. Siempre que se pueda, la 
comunicación es cara a cara. 
- Feedback: al final de cada iteración se entrega un software ejecutable y 
válido. Se demuestra el software pronto y frecuentemente.
- Respeto: todo el mundo da y recibe respeto. Los programadores respetan la 
experiencia de los clientes y al revés.
- Coraje: siempre se dice la verdad sobre las estimaciones y el estado de las 
tareas.

## Para seguir leyendo

- [Principio de oxidación del software (Spanish)](http://www.adictosaltrabajo.com/detalle-noticia.php?noticia=379)
- [Barry Boehm](https://en.wikipedia.org/wiki/Barry_Boehm)
- [XP lessons learned](http://www.extremeprogramming.org/lessons.html)
- [When should XP be used](http://www.extremeprogramming.org/when.html)
- [Agile process](http://www.agile-process.org)
- [Extreme programming explained](http://www.amazon.com/Extreme-Programming-Explained-Embrace-Edition/dp/0321278658)

[eXtreme Programming]: http://www.extremeprogramming.org

