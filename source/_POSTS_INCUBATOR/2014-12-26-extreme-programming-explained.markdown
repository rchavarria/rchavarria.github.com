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
- code also gives you a chance
