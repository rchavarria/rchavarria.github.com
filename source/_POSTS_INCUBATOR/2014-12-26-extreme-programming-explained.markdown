# Extreme Programming explained, by Kent Beck

- Extreme Programming (XP) is a lightweight methodology for small-to-medium-sized teams developing software in the face of vague or reapidly changing requirements
- XP is an experiment to answer the question: "How would you program if you had enough time?" -> Mentality of sufficiency Vs. Mentality of scarcity : parábola de la tribu del bosque y la de la montaña
- Most of the practices in XP are as old as programming

## Part I: the problem

- The basic problem is risk
- How does XP address the risk?

1. Schedule slips: short release cycles
2. Project canceled: asks the customer to choose the smallest release that makes the most business sense
3. System goes sour: Cruft is not allowed to accumulate
4. Defect rate: tests functions and program features
5. Business misunderstood: customer to be an integral part of the team
6. Business changes: shortens the release cycle
7. False feature rich: highest priority tasks are addressed
8. Staff turnover programmers to accept responsibility

- XP puede ayudar en varios aspectos para una estrategia para maximizar el valor económico del proyecto:

1. Spending money and earning sooner
2. Increasing the probability that the project will stay alive

- There are four variables in soft dev: **Cost**, **Time**, **Quality**, **Scope**.
- customers and managers pick values for three of them, the development team gets to pick the resultant value of the fourth variable
- If the don't like the result they can change the inputs or they can pick a different three variables to control
- In many ways, cost is the most constrained variable. The investment has to start slow and grow over time
- Quality is a strange variable. Often, by insisting on better quality you can get projects done sooner. temporarily sacrificing internal quality to reduce time to market is a tempting short-term play. Pero hay que tener cuidado o la falta de calidad te pillará y puede que llegues a un punto de código inmantenible.
- For software dev, **scope** is the most important variable to be aware of.
- What if we see the softness of requirements a s an opportuity, not a problem? Then we can choose to see scope as the easiest of the four variables to control, because it is so soft, we can shape it.
- ¿Cómo conseguir que no suba el coste del cambio con el paso del tiempo?

1. simple design
2. automated tests
3. constant refinement of the design

- We need to control the development of software by making many small adjustements, not by making a few large adjustments.
- haz muchos cambios pequeños (mejor que unos pocos grandes) pero nunca apartar los ojos de la carretera

- Four values

1. **Comunication**: problems with projects can invariably be traced back to somegody not talking to somebody else about somthing important. the effect of testing, pair programming and estimating is that programmers and customers and managers have to ocmmunicate
2. **Simplicity**: is not easy. it is the hardest thing in the world not to look toward the things you'll need to implement tomorrow andnext week and next month
3. **Feedback**: feedback works at different tme scales. unit tests give feedback in minutes or days. functional tests give feedback in weeks or months. The system is put into production as soon as it makes sense, so the business can begin to feel what the system is like. Feedback works with communication and simplicity. the more feedback you have, the easier it is to communicate. If yuoare communicating clearly, you will know what to test and measure. Simple systems are easier to test
4. **Courage**: cuando se dieron cuenta de que había que hacer algo duro, rompieron el flujo, rompieron la mitad de los tests. unos cuantos días de duro trabajo después, todos los tests volvían a estar bien. Otro movimiento de corage es el de desechar código. If you don't have the three first values in place, courage by itself is just palain hacking/cracking.

- Basic principles: a value may be vague. A principle s more concrete:

1. **Rapid feedback**: time between an action and its feedback is critical to learning (semanas mejor que meses, minutos mejor que dias)
2. **Assume simplicity**: treat every problem as if it can be solved with ridiculou simplicity. trust your ability to add complexity in the future where you need it
3. **Incrmental change**: any problem is solved with a series of the smallest changes that make a difference
4. **Embrace change**: 
5. **Quality work**: nobody likes working sloppy. everybody likes doing a good job. 

- Aquí hay otros principios,que no son tan céntricos como los anteriores, pero que tamibén se tienen en cuenta

6. **Teach learning**: en lugar de adoctinar, o mandar, se pueden suerir estrategias, lecturas, para que cada uno aprenda sus lecciones.
7. **Small initial investment**: the focus a tight budget generates encourages you to do a good job of everything you do, pero no recortes mucho, o no podrás hacer nada interesante
8. **Play to win**: en lugar de trabajar *según el manual* (para que cuando todo acabe no te puedan echar la culpa del fracaso), en XP cada miembro del equipo hace lo que está en su mano para ayudar al equipo a ganar
9. **Concrete experiments**: cada vez aque tomas una decisión y no la compruebas (con un experimento) puedes haber tomado la decisión incorrecta
10. **Open, honest communication**: los programadores deben de ser libres de reportar malas noticias a clientes y managers, de entregarlas pronto y de no ser castigados por ello
11. **Work with people's instincts, not against them**: you can expound all you want on some practice (the best practice you know), but when the pressure mounts, if the practice doesn't sove an immediate problem it will be discarded.
12. **Accepted responsibility**: if the team comes to the conclusion that a ertain task needs doing, someone will choose to do ti, no matter how odious
13. **Local adaptation**: you get to decide how to develop. You have to change and adapt.
14. **Travel light**: they just carry what they must have to keep producing value for the customer (tests and code)
15. **Honest measurement**: specially of working hours

## Back to basics

**Coding**

Es la única actividad con la que sabemos que sin ella no podemos tener software. Escribir código simplemente está bien para pequeños programas, pero para appliaciones más complejas necesitamos algo más allá de la programación.
- code also gives you a chance to communicate clearly and concisely. if you have an idea and explain it to me, I can easily misunderstand. if we code it together, I can see in the logic you write the precise shape of you ideas. this communication easily turns into learning. I see your idea and I get one of y own. I turn to code, also.
- ya que no podemos prescindir del código (ya que si no no existiría el programa), we should use it for as many purposes of software engineering as possible: communicate, describe algorithms, tests and specifications

**Testing**

- Cualquier cosa que no puede ser testeada, no existe. PUedes creer que has implementado tu diea,pero si no puedes probarla, ¿cómo puedes estar seguro?
- tmabien se pueden escribir tests para requerimientos no-funcionales: performances, adhere of code to standards
- the tests tell you when you're done. when you can't htink of any tests to write that might break, you're completely done
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




