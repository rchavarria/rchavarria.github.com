# Extreme Programming explained, by Kent Beck

- Extreme Programming (XP, o Programación Extrema) es una metodología ligera 
para equipos de tamaño pequeño o mediano que desarrollan software 
enfrentándose a requisitos vagos o en contínuo cambio.
- XP es un experimento para responder a la pregunta: ¿Cómo programarías si
tuvieras suficiente tiempo? Donde se explica la diferencia entre la *Mentalidad
de la suficiencia* frente a la *Mentalidad de la escasez* (parábola de la
tribu del bosque y de la montaña)
- La mayoría de las prácticas en XP son tan viejas como la programación en
sí misma.

## Part I: the problem

- El problema básico es el riesgo, así que, ¿cómo gestiona XP el riesgo?

1. Desviaciones de la planificación: ciclos de releases cortos
2. Cancelación del proyecto: pregunta al cliente que elija la release más pequeña
que tiene sentido para el negocio
/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\                          
3. System goes sour: Cruft is not allowed to accumulate
/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\/!\                          
4. Tasa de defectos: teste funciones y funcionalidades
5. Malentendido en el negocio: el cliente es una parte integral del equipo
6. Cambios en el negocio: ciclos de releases cortos
7. Falsa riqueza de funcionalidades: se realizan las tareas con la máxima prioridad
8. Rotación del personal: los programadores aceptan responsabilidades

- XP puede ayudar en varios aspectos para una estrategia para maximizar el 
valor económico del proyecto:

1. Gastando menos dinero y generando ingresos antes
2. Incrementando la probabilidad de que el proyecto siga con vida durante más tiempo

- Hay cuatro variables fundamentales en el desarrollo software: **Coste**, **Tiempo**,
**Calidad** y **Alcance**.
- Clientes y Managers escogen los valores de tres de ellas, el equipo de desarrollo
elige el valor resultante de la cuarta.
- Si no les gusta el resultado, pueden cambiar los valores de entrada o pueden 
elegir otras tres variables de control distintas.
- En la mayoría de los casos, el Coste es la variable más restrictiva. La inversión
comenzar poco a poco y crecer a lo largo del tiempo.
- La Calidad es una variable extraña. A menudo, insistir en una mejor Calidad
puede hacer que los proyectos estén hechos antes. Los sacrificios internos de
Calidad de forma temporal para reducir el tiempo de entrega puede ser una
forma tentativa de jugar. Pero hay que tener cuidado o la falta de calidad
te pillará y puede que llegues a un punto de código inmantenible.
- En cuanto al desarrollo del software, el **Alcance** es la variable más importante
a tener en cuenta.
- ¿Qué tal si vemos la flexibilidad de los requisitos como una oportunidad y no
como un problema? Así podemos ver el Ámbito como la más fácil de las cuatro variables
de control, porque es tan flexible que podemos darle la forma que queramos.
- ¿Cómo conseguir que no suba el coste del cambio con el paso del tiempo?

1. Diseño sencillo
2. Tests automáticos
3. Refinamiento constante del diseño

- Necesitamos controlar el desarrollo del software mediante muchos pequeños ajustes,
no con unos pocos ajustes muy grandes.
- Haz muchos cambios pequeños (mejor que unos pocos grandes) pero nunca apartar
los ojos de la carretera (porque desarrollar es como conducir, es mejor ir haciendo
pequeñas correcciones que un volantazo para corregir el rumbo).

## Los cuatro valores

**Comunicación**

- Cualquier problema en un proyecto puede, invariantemente, ser
rastreado hasta encontrar a alguien que no habló con otro alguien acerca de algo
importante. 
- El efecto de los tests, programación en parejas y las estimaciones es que
Programadores, Clientes y Managers están obligados a comunicarse.

**Simplicidad**

- La Simplicidad no es fácil.
- Lo más difícil en el mundo es evitar mirar hacia adelante al pensar en funcionalidades
que vas a necesitar implementar mañana, la próxima semana o el próximo mes.

**Feedback**

- Trabaja en diferentes escalas de tiempos. Por ejemplo, los tests unitarios dan
feedback en minutos o días, mientras que los tests funcionales proporcionan feedback
en semanas o meses.
- El sistemas se pone en producción tan pronto como tiene sentido hacerlo. De esta
forma el Negocio puede comenzar a ver cómo va a ser el sistema.
- El feedback funciona con la Comunicación y la Simplicidad. Cuanto más feedback
tienes, más fácil es comunicar. Si estás comunicando claramente, sabrás qué debes
medir y testear. Los sistemas simples son más fáciles de testear.

**Coraje**

- En ocasiones, hay que saltarse las normas, romper el flujo, romper la mitad
de los tests. Después de unos días de duro trabajo (y coraje), los tests
deberían volver a estar bien.
- Otro movimiento de coraje es el de desechar código.
- Si no tienes los tres primeros valores en su lugar, el Coraje por sí mismo
no es más que hackear y crackear el sistema.

## Principios básicos

Un valor puede ser vago, un principio es más concreto.

1. **Feedback rápido**: el tiempo entre una acción y su feedback es crítico
para aprender (semanas mejor que meses, minutos mejor que dias).
2. **Asumir simplicidad**: tratar cualquier problema como si pudiera ser resuelto
con una simplicidad ridícula. Confía en tu habilidad para añadir complejidad en
el futuro, cuando realmente la necesites.
3. **Cambio incremental**: cualquier problemas se resuelve con una serie de
cambios pequeños que poco a poco van marcando la diferencia.
4. **Acepta el cambio**
5. **Trabajo de calidad**: a nadie le gusta un trabajo descuidado, a todo el
mundo le gusta hacer un buen trabajo.

Existen otros principios, que no son tan céntricos como los anteriores, pero
que tamibén se tienen en cuenta:

6. **Enseña a aprender**: en lugar de adoctinar, o mandar, se pueden suerir
estrategias, lecturas, para que cada uno aprenda sus lecciones.
7. **Inversión inicial pequeña**: el foco que un presupuesto ajustado genera
te incentiva a hacer un excelente trabajo en todo lo que haces, pero no recortes
mucho o no podrás hacer nada interesante.
8. **Juega para ganar**: en lugar de trabajar *según el manual* (para que cuando
todo acabe no te puedan echar la culpa del fracaso), en XP cada miembro del
equipo hace lo que está en su mano para ayudar al equipo a ganar.
9. **Experimentos concretos**: cada vez aque tomas una decisión y no la
compruebas (con un experimento) puedes haber tomado la decisión incorrecta.
10. **Comunicación honesta y abierta**: los programadores deben de ser libres
de reportar malas noticias a clientes y managers, de entregarlas pronto y
de no ser castigados por ello.
11. **Trabaja con los instintos de la gente, no contra ellos**: puedes hacer
incapié todo lo que quieras sobre una buena práctica (quizá la mejor que conozcas),
pero cuando la presión hace efecto, si la práctica no arregla un problema
inmediato será descartada por la gente.
12. **Aceptar responsabilidad**: si el equipo llega a la conclusión de que cierta
tarea debe ser hecha, alguien elegirá hacerla, aunque sea la peor tarea del
mundo.
13. **Adaptación local**: no hay que seguir todas las normas a rajatabla, tú debes
decidir cómo hacer software. Cambia, mide y adapta lo que mejor trabaje para ti.
14. **Viaja ligero**: el equipo solo arrastra lo que deban arrastar para producir
valor al cliente, normalmente, solo código y tests.
15. **Mediciones honestas**: especialemente las horas trabajadas.

## Vuelta a lo básico

**Codificar**

- Es la única actividad con la que sabemos que sin ella no podemos tener software.
Escribir código simplemente está bien para pequeños programas, pero para
appliaciones más complejas necesitamos algo más allá de la programación.
- El código te da la oportunidad de comunicarte clara y concisamente. Si tienes una
idea y me la explicas, probablemente yo te malinterprete. Si la codificamos juntos,
puedo ver tus ideas en la lógica que escribes. Esta comunciación se transforma
fácilmente en aprendizaje. Veo tus ideas y tengo las mias propias. Así que ahora
es mi turno de codificar y enseñarte mis ideas.
- Ya que no podemos prescindir del código (ya que si no no existiría el programa),
deberíamos usarlo para tantos propósitos sobre ingenieria del software como fuera
posible: comunicar, describir algoritmos, tests, especificaciones, ...

**Testear**

- Cualquier cosa que no puede ser testeada, no existe. PUedes creer que has
implementado tu diea,pero si no puedes probarla, ¿cómo puedes estar seguro?
- También se pueden escribir tests para requerimientos no-funcionales:
rendimiento, cumplimentación de estándares de codificación, ...
- Los tests te dicen cuando has terminado. Cuando ya no puedes pensar en
ningún test erróneo más, es cuando has terminado completamente (ya no tienes
ningún código de producción más que escribir).
- most software ships withou testss. automated tests clarly aren¡t essential, entonces porqué considerarlo como una actividad básica?
- long-term answer is taht tests keep the program alive longer, you can make nore changeslonger
- short-term reason: programming with tests is more fun. you code with so much more confidence

**Listening**

- como programador, no sabes nada del negocio, así que debes preguntar. if you're going to ask questions, then you'd better be prepared to listen to the answers
- programmers help the customer to understandwhat is hard and what is easy
- the things that have to be communicated get communicated when they need to be communicated an in the amount of deeetail they need to be communicated.

**Designing**

- designing s creating a structure that organizes the logic in the system
- good design: a change in one part of the system doesn't always require a change in another part of the system. ensures that every piece of logic in the system has one and only one home. puts the logic near the data it operates on. allows the extension of the system with changes in only one place

**Conclusion**

You code because you want some software. You test to know whne you're done coding. You lisen to know what to code or what to eest. YOu design to keep coding and testing and listening indefinitely.

## Part II: the solution

Prácticas

**Planning game**

- Qué es lo que se va a entregar (planning game) es una mezcla entre las prioridades del negocio y las estimaciones técnicas.

**Small releases**

- every release should be as small as possible, containng the most valuable business requirements

**Metaphor**

- the metaphor just helps everyone on the project understand the basic elements and their relationshsiops
- by asking for a metaphor we are likely to get an architecture that is easy to commujnicate and elaborate

**Simple design**

- runs all teh tests. has no duplicated logic. states every intention imporatant to hgt programmers. has the fewest possible clases and methods (lements)

**Testing**

- any program featue without an automated test simply doesn't exist. unit and functional tests. the reuslt is a program that becoes more and more confident over time  it becomes more capable of accepting change

**Refactoring**

- after they had added the feature, the programmers ask if they now can see how to tmake the program simpler, while still runningn all of the tests
- you don't refactor on specullaiton. you  refactor whne hte system asks you to. when the system requires that you dupliczte code, it is aksing for refactoring

**Pair programmign**

- two roles: on is thinkinig about the best way to impleent this methdo right here. the other is thingkin more strategically

**Collective ownership**

- anybdoy who sees an opporunity to add value to any portion of the code is requiered to do so at any time

**Continuous integartion**

- code is integrated and tested lots of times a day

**40-hour week**

- i want to be fresh and eager every morning, and tired and satisfied every night. overitem is a symptom of a seriuos problem on the project.

**On-site customer**

- a real customer must sit with the team, availble to answer questions, resolve disputes, ans set small-scale priorities.

**Coding standards**

- the standard must be adopted voluntarily by the whole team


- Cómo unas prácticas refuerzan las debilidades del resto de ellas:

1. planning game: es apoyado por on-site customer, short releases
2. short releases: le apoya planning game, continuous integrations, tests and simple design
3. metaphor: tests, on-site customer, refactoring
4. simple design: refactoring, metaphor, pair programming
5. testing: simple design, pair programming
6. refactoring: collective ownership, coding standards, pair programming, simple design, ,tests, continuous integrations, 40-hour week
7. pair programming: coding standards, 40-hour week, metaphor, tests, simple design
8. collective ownership: continuous integration, tests, pair programming, coding standards
9. continuous integration: tests, pair programmming, refactoring
10. 40-hour week: todas las prácticas llevan a trabajr jornadas razonabeles
11. on-site ucstomer: they write functional tests, make small-scale priority and decisions
12. coding standards: pair programming, refactoirng

/!\  imagencita de la página 58 sobre todas las prácticas interconectadas /!\

### management strategy

- manager's job is to highlight what needs to be done, no tto assign work
- manager provides guidance all along
- namanger needstotake the leas in adapting XP to lclal conditions
- manager doesn't impose a lot of overhead (burocracia)

**metrics**

- tha basic XP manangement tool is the metric
- the medium of the metric is the Big Visible Chart, the manager periodically updates aprominnent chart
- don't have too many metrics, and be prepared to retie metrics that have served their purpose
- any metric that is approaching 100% is likely to be useless

**coaching**

- management is divided into two roles: the coach and the tracker. coaching is primarily concerned with the technical execution and evolution of the process

**tracking**

- if you don't measure what really happens against what you predicted would happen, you won't ever learn
- planning is always emotional

**intervention**

- cuando hay problemas que el equipo nop uede solucionar, es el manager quien tiene que interverni, pero con cuidado, si abasallar, o perderá toda la confianza
- ejemplos: cambios de personal, se necesitan cambios en los procesos del equipo, matar el proyecto

## facilities strategy

- tking control of the physical environment sends a powerful message to the team. 
- taking control of their physical environment is the first step toward taking control of hwo they work overall
- antoher wayof saying thi sis that the split of power between Business and Develoment is not an exucse to avoid tough jobs
- most of the time the work will be simpler than you first imagined. whne it isn't, you do it anyway, beause that is what you get paid for

## planning strategy

- we wil make the plan quickly and cheaplly, so there will be little inertia when we must change it
- primero, aprende las reglas y síguelas (como estas para planificar). cuando estés cómodo con ellas, podrás saltártelas para mejorar
- the goal: the goal of the game is to maximize the value of software produced by the team
- the strategy: invest as little as possibl to put the most valuable functionality into production as quicklly as possible
- players: two players, Development and Business
- moves: exploration, commitment and steer (pequeños cambios frente a grandes cambios, como pequeñas correcciones conduciendo un coche)
- exploration phase: what all the system should eventually do. Write a story, Estimate a story, Split a story.
- commitment phase: Business choose the scope and date, Development confidently commit to delivering it (or not, so Business has to choose another scope or date). Sort by value, Sort by risk, Set velocity, Choose scope
- steering phase: update the plan based on what is learned. Iteration, Recovery, New story, Reestimate

## iteration planing

- pieces are task cards instead of story cards, but movements are  quite similar
- exploration phase: Write a task, Split/Combine tasks
- commitment phase: Accept a task, Estimate a task, Set load factors, Balancing
- steering phase: Implement a task, Record progress, Recovery, Verify story

## development strategy

- while you are developing, you can act like you and your partner are the only pair on th eproject. then you switch hats. as integrators, you become aware where there are collisions
- Collective ownership: one of the effects of collective ownership is that complex code does not live very long. It tends to spread knowledge of the system around the team
- pair programming: it isn't a person programming whiole another person watches. it's a dialog trying to simultaneously program, analyze, design and test. it works for XP becuase it encourages communication

## design strategy

- hay dos problemas con lo de diseñar para un futuro: 

1. las especificaciones pueden cambiar (por lo que el diseño ya no vale para nada)
2. puedes aprender una mejor manera de hacer las cosas. 

si no pasa una dde las dos, es mejor diseñar para el futuro pero **yo no me arriesgo** a que no haya cambios y mucho menos a no aprender nada.

- when faced iwth a big refactoring, you have to take it in small steps. mientras estás desarrollando, ves la oporutnidad de hacer un peuqeño cambio. Hazlo. La gran refactoización se irá reduciendo.

- four rules of simple design:

1. systme (code and test) must communicate everything you want to communicate
2. system must contain no duplicate code
3. system should have the fewst possible classes
4. system should have the fewest possible methods

### roles of pictures in design

- benefits: if you find it impossible to reduce the number of elements, if there is an obvious asymmetry, if there are many more lines than boxes. all of these are clues to a bad design. Another strength is speed
- cons: they can't give you concrete feedback
- the pictures aren't saved. wishing you could save the whiteboard is a sure sign the design hasn't been communicated, either to the theam or to the system

## testing strategy

- los tests escritos por unos dan confianza al resto del equipo
- se puede aprender de los ests, en dos casos: 

1. tests debería fallar y no falla -> código mal
2. tests no debería fallar y falla -> código mal

- the tester's job is to translage the sometimes vague testing ideas of the customer into real, automatic, isolated tests

# Part III: implementing XP

## adoptin XP

- how to adopt: pick your worst problem, solve it the XP way, when it's no longer your worst problem, repeat.

## retrofitting XP

- ¿cómo comenzar a escribir tests para un código que ya existe? ¿todo de golpe? No, poco a poco

## roles for people

### programmer

- your job isn't over when the computer understnds what to do. your first value is communication with other people
- una habilidad necesaria es *pair programming*
- another skill needed by the extreme programmer is the habit of simplicity
- tienes que estar dispuesto a aceptar la propiedad colectiva del código
- without courage, XP just simply doesn't work

### customer

- the programmer knows how to program. the customer knows what to program.
- skills for the custormer to be learned: write good stories, influence a project without being able to congtrol it
- customers have to make decisions
- you will have to learn how to write stories
- you will have to learn to write functional tests

### tester

- you are responsible fo rhelping the customer choose and write functional testss

### tracker

- you have to make lots of estimates and then notice how reality conformed to your guesses. 
- your job is to close the loop on feedback
- kkeping an eye on the big picutre
- your are the team historian. keep a log of functional test scores and defects reported
- the skill you need to cultivate most is the ability to collect the information you need without distrubing

### coach

- you notice when people are deviating from the team's process and bring this to the team's attention
- how other teams are using XP, what the ideas behind XP are, and how they realte to the current situation
- confident, aggressive programmers are valuable precisely because they are confident and aggressive

### consultant

- los equipos XP son my buenos técnicamente, pero de bez en cuando necesitan a un experto
- what they won't do is let you go off and sole the problem by yourseelf
- and when you are done, they will most likely throw away eveythingyou have done and do it over tehmselves

## 20-80 rule

## what makes XP hard

- it is primarily emotions (espeically fear) that makes XP hard
- you have to learn to be dissatisfied with coplexity, not to rest until you can't imagin anything simpler working
- las emociones forma parte de las persones, por eso, XP no trata de eliminarlas sino que acepta e incentiva que las personas expersen sus sentimientos

## when you hsouldn't try XP

- the giggest barrrer to the succes sof an XP project is business culture
- another culture that is not conducive to XP is one in which you are required to put in long hours to prove your "commitment to the company"

## xp at work

- 


