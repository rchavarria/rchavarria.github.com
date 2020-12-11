Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 27 | posición 403-403 | Añadido el lunes, 24 de diciembre de 2018 20:12:53

1.1 Why Domain-Driven Design?
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 27 | posición 412-412 | Añadido el lunes, 24 de diciembre de 2018 20:13:02

1.2 How Domain-Driven Design helps?
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La nota en la página 27 | posición 414 | Añadido el lunes, 24 de diciembre de 2018 20:13:17

Y bounded contexts
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 27 | posición 413-414 | Añadido el lunes, 24 de diciembre de 2018 20:13:17

1. Ubiquitous Language:
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 28 | posición 419-420 | Añadido el lunes, 24 de diciembre de 2018 20:14:02

2. Strategic Design: Domain-Driven Design addresses the strategy behind the direction of the business, not just the technical aspects.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 28 | posición 422-423 | Añadido el lunes, 24 de diciembre de 2018 20:14:18

3. Tactical Design: Domain-Driven Design provides the tools and the building blocks for iterative software deliverables.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 28 | posición 424-425 | Añadido el lunes, 24 de diciembre de 2018 20:14:25

1.2.1 Ubiquitous Language
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 28 | posición 426-427 | Añadido el lunes, 24 de diciembre de 2018 20:14:35

consider a Bounded Context is a conceptual boundary around a system.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 28 | posición 427-428 | Añadido el lunes, 24 de diciembre de 2018 20:15:26

The Ubiquitous Language inside a boundary has a specific contextual meaning. Concepts out of this context can have a different meaning.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 29 | posición 431-432 | Añadido el lunes, 24 de diciembre de 2018 20:15:33

1.3 Should I start considering Domain-Driven Design as an option?
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 29 | posición 444-445 | Añadido el lunes, 24 de diciembre de 2018 20:16:46

1.4 Main challenges of applying Domain-Driven Design
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 30 | posición 453-453 | Añadido el lunes, 24 de diciembre de 2018 20:18:37

1.5 The business value of using Domain-Driven Design
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 30 | posición 458-458 | Añadido el lunes, 24 de diciembre de 2018 20:19:24

1.6 Wrap-up
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 31 | posición 473-473 | Añadido el lunes, 24 de diciembre de 2018 20:20:27

2. Architectural Styles
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 32 | posición 484-484 | Añadido el lunes, 24 de diciembre de 2018 20:21:28

2.1 The Good Old Times
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 36 | posición 542-542 | Añadido el lunes, 24 de diciembre de 2018 20:23:53

2.2 Layered Architecture
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 37 | posición 557-557 | Añadido el lunes, 24 de diciembre de 2018 20:25:07

2.2.1 Model-View-Controller
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 39 | posición 598-601 | Añadido el lunes, 24 de diciembre de 2018 20:29:34

an Application Service and its purpose is to orchestrate and organize the domain behaviour. In other words, the Application services are the ones that make things happen and they are the direct clients of a Domain Model. No other type of object should be able to directly talk to the internal layers of the Model layer.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 40 | posición 604-605 | Añadido el lunes, 24 de diciembre de 2018 21:01:19

the View layer receives an object, often a Data Transfer Object (DTO)
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 40 | posición 609-611 | Añadido el lunes, 24 de diciembre de 2018 21:01:31

Why create a DTO instead of giving an instance of the Model to the View layer? The main reason and the short answer is, again, Separation of Concerns.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 42 | posición 636-638 | Añadido el lunes, 24 de diciembre de 2018 21:04:24

In terms of a web application in PHP, the Controller usually comprehends a set of classes, which in order to fulfill their purpose “speak HTTP” . That is, they receive an HTTP request and return an HTTP response.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La nota en la página 42 | posición 638 | Añadido el lunes, 24 de diciembre de 2018 21:04:51

El controlador no es solo una clae. O una config
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 43 | posición 651-652 | Añadido el lunes, 24 de diciembre de 2018 21:10:54

2.3 Inverting Dependencies. Hexagonal Architecture
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 43 | posición 658-661 | Añadido el lunes, 24 de diciembre de 2018 21:19:47

As the Domain Model layer depends on concrete infrastructure implementa- tions, the Dependency Inversion Principle⁷ could be applied by relocating the Infrastructure layer on top of the other three layers.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 44 | posición 666-668 | Añadido el lunes, 24 de diciembre de 2018 21:20:17

the Infrastructure layer which can be referred to as low level modules now depend on the UI, the Application Layer and the Domain Layer, which are the high level modules. The dependency has been inverted.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 44 | posición 669-669 | Añadido el lunes, 24 de diciembre de 2018 21:20:55

what is Hexagonal Architecture?, and how does it fit within of all this?
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 44 | posición 672-673 | Añadido el lunes, 24 de diciembre de 2018 21:21:05

In terms of the DIP, the Port would be a high level module and an Adapter would be a low level module.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 47 | posición 712-713 | Añadido el lunes, 24 de diciembre de 2018 21:25:12

2.4 Command Query Responsibility Segregation
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 48 | posición 734-738 | Añadido el lunes, 24 de diciembre de 2018 21:32:26

CQRS seeks an even more aggressive separation of concerns splitting the Model in two: • The Write Model: Also known as the Command Model, it performs the writes and takes responsibility for the true domain behaviour. • The Read Model: It takes responsibility of the reads within the application and treats them as something that should be out of the Domain Model.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 49 | posición 740-741 | Añadido el lunes, 24 de diciembre de 2018 21:32:47

This strict separation triggers another problem, Eventual Consistency.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 49 | posición 748-749 | Añadido el lunes, 24 de diciembre de 2018 21:33:50

there should be a process that updates the cache system. Cache systems are eventually consistent.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 49 | posición 749-750 | Añadido el lunes, 24 de diciembre de 2018 21:34:01

This kind of processes, speaking in CQRS terminology, are called Write Model Projections or just Projections.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 49 | posición 751-753 | Añadido el lunes, 24 de diciembre de 2018 21:34:44

This process can be synchronous or asynchronous, depending on your needs, and it can be done thanks to another useful tactical design pattern that will be explained in detail later on in the book, Domain Events.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 50 | posición 755-755 | Añadido el lunes, 24 de diciembre de 2018 21:35:09

2.4.1 The Write Model
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- El marcador en la página 49 | posición 748 | Añadido el lunes, 24 de diciembre de 2018 21:35:13


==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 50 | posición 755-755 | Añadido el jueves, 27 de diciembre de 2018 23:47:15

true holder of domain behaviour.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 50 | posición 760-761 | Añadido el jueves, 27 de diciembre de 2018 23:47:39

Post model, leaving it only with command methods. This means we will effectively get rid of all the getter methods
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 50 | posición 762-763 | Añadido el jueves, 27 de diciembre de 2018 23:48:59

domain events will be published in order to be able to trigger write model projections by subscribing to them.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 53 | posición 806-806 | Añadido el jueves, 27 de diciembre de 2018 23:50:59

2.4.2 The Read Model
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 55 | posición 829-829 | Añadido el jueves, 27 de diciembre de 2018 23:54:29

the read model should be completely disposable
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 55 | posición 830-831 | Añadido el jueves, 27 de diciembre de 2018 23:54:53

can be removed and recreated when needed using write model projections.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 56 | posición 851-851 | Añadido el jueves, 27 de diciembre de 2018 23:58:16

2.4.3 Synchronizing the Write Model with the Read Model
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 56 | posición 853-854 | Añadido el viernes, 28 de diciembre de 2018 0:07:27

For each type of domain event captured, a specific projection will be executed.
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- La subrayado en la página 60 | posición 913-913 | Añadido el viernes, 28 de diciembre de 2018 0:10:23

2.5 Event Sourcing
==========
Domain-Driven Design in PHP (Carlos Buenosvinos, Christian Soronellas;Keyvan Akbary)
- El marcador en la página 60 | posición 912 | Añadido el viernes, 28 de diciembre de 2018 0:11:49


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 24 | posición 355-355 | Añadido el lunes, 9 de abril de 2018 2:16:07

Chapter
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 24 | posición 355-355 | Añadido el lunes, 9 de abril de 2018 2:16:23

Chapter 1. Why Plan?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 24 | posición 358-359 | Añadido el lunes, 9 de abril de 2018 2:17:02

We plan to ensure that we are always doing the most important thing left to do, to coordinate effectively with other people, and to respond quickly to unexpected events.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 25 | posición 369-370 | Añadido el lunes, 9 de abril de 2018 2:18:06

Why We Should Plan
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 26 | posición 397-397 | Añadido el lunes, 9 de abril de 2018 2:21:56

Planning allows us both to adjust what we do and to coordinate with
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 26 | posición 397-397 | Añadido el lunes, 9 de abril de 2018 2:22:01

Planning allows us both to adjust what we do and to coordinate with others.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 27 | posición 401-401 | Añadido el lunes, 9 de abril de 2018 2:23:18

What We Need in Planning
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 27 | posición 406-406 | Añadido el lunes, 9 de abril de 2018 2:24:07

In order to carry out the coordination it's vital to have an accurate picture of how far you are along in the plan.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 27 | posición 412-412 | Añadido el lunes, 9 de abril de 2018 2:24:50

Any software planning technique must try to create visibility,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 27 | posición 413-413 | Añadido el lunes, 9 de abril de 2018 2:25:53

This means that you need clear milestones,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 28 | posición 419-420 | Añadido el lunes, 9 de abril de 2018 2:26:02

The Planning Trap
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 28 | posición 424-425 | Añadido el lunes, 9 de abril de 2018 2:27:06

If things don't go according to plan, then the planner is afraid he will be blamed. That fear induces the planner to say that the plan is still on track.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 29 | posición 432-433 | Añadido el lunes, 9 de abril de 2018 2:27:52

Events happen. Plans change.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 29 | posición 435-436 | Añadido el lunes, 9 de abril de 2018 2:28:28

Chapter
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 31 | posición 466-467 | Añadido el lunes, 9 de abril de 2018 2:30:24

Unacknowledged Fear Is the Source of All Software Project Failures
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 31 | posición 467-468 | Añadido el lunes, 9 de abril de 2018 2:31:07

If these fears are not put on the table and dealt with, then developers and customer each try to protect themselves by building walls.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 31 | posición 474-475 | Añadido el lunes, 9 de abril de 2018 2:31:20

Customer Bill of Rights
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 32 | posición 483-483 | Añadido el lunes, 9 de abril de 2018 2:31:32

Programmer Bill of Rights
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 32 | posición 489-490 | Añadido el lunes, 9 de abril de 2018 2:31:51

we must create a culture that makes it possible for programmers and customers to acknowledge their fears and accept their rights and responsibilities.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 33 | posición 496-496 | Añadido el lunes, 9 de abril de 2018 2:32:39

Chapter 3. Driving Software
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 35 | posición 527-527 | Añadido el lunes, 9 de abril de 2018 2:35:50

Chapter 4. Balancing Power
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 35 | posición 527 | Añadido el lunes, 9 de abril de 2018 2:37:33


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 35 | posición 530-532 | Añadido el lunes, 9 de abril de 2018 2:46:15

Our planning process relies on clearly separating the roles of business people and software people. This ensures that business people make all the business decisions and software people make all the technical decisions.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 36 | posición 542-543 | Añadido el lunes, 9 de abril de 2018 2:48:00

estimating is a technical decision.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 36 | posición 549-550 | Añadido el lunes, 9 de abril de 2018 2:48:08

Choosing the relative priority between features is a business decision.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 36 | posición 550 | Añadido el lunes, 9 de abril de 2018 2:48:32

Asi que nada de elegir una tecnolohia porque sea cool
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 37 | posición 553-555 | Añadido el lunes, 9 de abril de 2018 2:49:05

Business decisions in planning are Dates Scope Priority
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 37 | posición 556-559 | Añadido el lunes, 9 de abril de 2018 2:49:16

Technical decisions in planning are Estimates If we have the right people making the decisions, planning will go as well as possible. We'll be able to deal with our disasters. We'll do it by reducing the number of disasters as much as possible, by finding out about the disasters as quickly as possible, and by maintaining as many
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 37 | posición 556-557 | Añadido el lunes, 9 de abril de 2018 2:49:25

Technical decisions in planning are Estimates
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 37 | posición 563-563 | Añadido el lunes, 9 de abril de 2018 2:50:08

The Customer
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 37 | posición 564-564 | Añadido el lunes, 9 de abril de 2018 2:51:00

By customer we mean the person who makes the business decisions.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 38 | posición 569-570 | Añadido el lunes, 9 de abril de 2018 2:51:23

XP planning assumes that the customer is very much part of the team,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 38 | posición 571-571 | Añadido el lunes, 9 de abril de 2018 2:51:29

Any (XP) project will fail if the customer isn't able to steer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 38 | posición 574-575 | Añadido el lunes, 9 de abril de 2018 2:51:51

Finding a Customer
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 38 | posición 581-581 | Añadido el lunes, 9 de abril de 2018 2:52:50

Is willing to accept ultimate responsibility
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 38 | posición 581-582 | Añadido el lunes, 9 de abril de 2018 2:52:55

Is willing to accept ultimate responsibility for the success or failure of the project
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 38 | posición 582 | Añadido el lunes, 9 de abril de 2018 2:53:18

Nada d esconderse bajo una pila de requisitos 
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 39 | posición 588-588 | Añadido el lunes, 9 de abril de 2018 2:53:45

Guiding the Customer
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 39 | posición 591-591 | Añadido el lunes, 9 de abril de 2018 2:55:06

Trust the developers' estimates,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 39 | posición 592-592 | Añadido el lunes, 9 de abril de 2018 2:55:08

Never let a date slip.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 39 | posición 594-595 | Añadido el lunes, 9 de abril de 2018 2:55:18

Provide a little valuable functionality every single release,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 39 | posición 598-599 | Añadido el lunes, 9 de abril de 2018 2:56:00

Chapter 5. Overviews
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 40 | posición 604-604 | Añadido el lunes, 9 de abril de 2018 2:57:08

Top Down
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 40 | posición 605-606 | Añadido el lunes, 9 de abril de 2018 2:58:16

cycles. Software development is no different. The planning challenge is that there are two cycles that we need to accommodate and synchronizethe business cycle and the development cycle.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 40 | posición 605-606 | Añadido el lunes, 9 de abril de 2018 2:58:21

The planning challenge is that there are two cycles that we need to accommodate and synchronizethe business cycle and the development cycle.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 40 | posición 611-611 | Añadido el lunes, 9 de abril de 2018 2:58:34

the business cycle is at least months long.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 40 | posición 612-613 | Añadido el lunes, 9 de abril de 2018 2:58:41

The development cycle has always been shorter than the business cycle.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 40 | posición 612 | Añadido el lunes, 9 de abril de 2018 3:00:43

Un ciclo de negocio es una release
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 40 | posición 612-612 | Añadido el lunes, 9 de abril de 2018 3:00:43

release.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 41 | posición 617-617 | Añadido el lunes, 9 de abril de 2018 3:00:56

development cycles an iteration.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 41 | posición 628-628 | Añadido el lunes, 9 de abril de 2018 3:01:24

Bottom Up
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 41 | posición 629-631 | Añadido el lunes, 9 de abril de 2018 3:02:12

What if we shrunk the whole software development life cycle to microscopic size, say two weeks? We would still have to solve all the problems we had to solve beforespecification, design, implementation, testing, integration, deployment, training, documentationbut now they would be small problems, not big problems, and some of them might disappear entirely.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 41 | posición 629-629 | Añadido el lunes, 9 de abril de 2018 3:02:28

What if we shrunk the whole software development life cycle to microscopic size, say two weeks?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 42 | posición 632-633 | Añadido el lunes, 9 de abril de 2018 3:02:32

We will have to do a little of each of them every day.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 42 | posición 638-639 | Añadido el lunes, 9 de abril de 2018 3:03:30

At the beginning of each iteration the business (remember the balance of power) will pick the most valuable features for the next iteration.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 42 | posición 643-643 | Añadido el lunes, 9 de abril de 2018 3:04:01

Chapter 6. Too Much to Do
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 42 | posición 644-645 | Añadido el martes, 10 de abril de 2018 2:09:58

When you are overloaded, don't think of it as not having enough time; think of it as having too much to do. You can't give yourself more time, but you can give yourself less to do,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 44 | posición 664-665 | Añadido el martes, 10 de abril de 2018 2:11:30

Chapter 7. Four Variables
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 44 | posición 670-674 | Añadido el martes, 10 de abril de 2018 2:12:57

In planning software projects, we had to add a variable before we could bring our projects under control: Cost Quality Time Scope We like to think of them as four levers on some big Victorian steam machine. The
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 44 | posición 667-668 | Añadido el martes, 10 de abril de 2018 2:13:06

We use four variables to help us think about how to control a project: cost, quality, time, and scope. They are interrelated but affect each other in strange ways.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 675-676 | Añadido el martes, 10 de abril de 2018 2:13:13

is that the effect of moving a lever is both delayed and nonlinear.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 676-677 | Añadido el martes, 10 de abril de 2018 2:13:33

hold everything else the same, and halve the time. So each lever gets its own little instruction manual.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 676-677 | Añadido el martes, 10 de abril de 2018 2:13:37

So each lever gets its own little instruction manual.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 45 | posición 677 | Añadido el martes, 10 de abril de 2018 2:14:02

Lever significa cada una de esas vbles
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 678-678 | Añadido el martes, 10 de abril de 2018 2:14:08

Cost
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 679-679 | Añadido el martes, 10 de abril de 2018 2:14:34

is actually several mostly independent levers.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 680-680 | Añadido el martes, 10 de abril de 2018 2:14:41

The most powerful lever is people.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 681-681 | Añadido el martes, 10 de abril de 2018 2:15:14

more people on the project. This lever, however, suffers from having both a nonlinear effect and a long delay.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 681-681 | Añadido el martes, 10 de abril de 2018 2:15:18

suffers from having both a nonlinear effect and a long delay.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 45 | posición 681-682 | Añadido el martes, 10 de abril de 2018 2:15:24

nonlinearity comes from the communication overhead
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 46 | posición 692-692 | Añadido el martes, 10 de abril de 2018 2:16:21

There are other ways to spend money. Spending on tools can be like adding people.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 46 | posición 695-696 | Añadido el martes, 10 de abril de 2018 2:16:43

Overtime doesn't help.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 46 | posición 696-697 | Añadido el martes, 10 de abril de 2018 2:17:01

for any length of time you will get bitten badly. The big killer is motivation. It's much better to have a motivated programmer work seven hours than a tired, distracted programmer work ten.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 46 | posición 696-697 | Añadido el martes, 10 de abril de 2018 2:17:04

The big killer is motivation. It's much better to have a motivated programmer work seven hours than a tired, distracted programmer work ten.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 46 | posición 702-703 | Añadido el martes, 10 de abril de 2018 2:17:41

Quality
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 46 | posición 703-703 | Añadido el martes, 10 de abril de 2018 2:17:46

Quality is really two levers: external and internal quality.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 46 | posición 703-704 | Añadido el martes, 10 de abril de 2018 2:17:57

External quality is the quality perceived by the customer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 709-710 | Añadido el martes, 10 de abril de 2018 2:18:35

internal quality. This reflects the quality of the internals of the system: how well it is designed, how good the internal tests are, and so on.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 712-712 | Añadido el martes, 10 de abril de 2018 2:18:59

Nothing kills speed more effectively than poor internal quality.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 714-715 | Añadido el martes, 10 de abril de 2018 2:19:15

Time and Scope
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 716-716 | Añadido el martes, 10 de abril de 2018 2:19:28

certainly impossible for exerting any short-term
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 716-716 | Añadido el martes, 10 de abril de 2018 2:19:33

certainly impossible for exerting any short-term control. Time and scope are left as the best levers to operate.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 716-716 | Añadido el martes, 10 de abril de 2018 2:19:40

Time and scope are left as the best levers to operate.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 718-719 | Añadido el martes, 10 de abril de 2018 2:20:26

they are placed on very different parts of the machine. The scope lever is right in front of you and just loves to be pushed up.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 47 | posición 719-719 | Añadido el martes, 10 de abril de 2018 2:20:30

machine. The scope lever is right in front of you and just loves to be pushed up.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 48 | posición 723-723 | Añadido el martes, 10 de abril de 2018 2:21:15

people don't usually realize what's happening until it's too late and the machine is out of control.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 48 | posición 723 | Añadido el martes, 10 de abril de 2018 2:21:38

La palanca del tiempo esta mmuy escpndida
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 48 | posición 724-724 | Añadido el martes, 10 de abril de 2018 2:21:43

Planning must make the time lever visible,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 48 | posición 725-726 | Añadido el martes, 10 de abril de 2018 2:22:18

You only really know where you are when you are at the end of project. So you need to end the project every few weeksthat's
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 48 | posición 734-735 | Añadido el martes, 10 de abril de 2018 2:22:37

Shopping for Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 50 | posición 757-757 | Añadido el martes, 10 de abril de 2018 2:24:17

Chapter 8. Yesterday's Weather
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 50 | posición 759-759 | Añadido el martes, 10 de abril de 2018 2:25:40

As the basis for your planning, assume you'll
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 50 | posición 759-760 | Añadido el martes, 10 de abril de 2018 2:25:47

As the basis for your planning, assume you'll do as much this week as you did last week.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 52 | posición 790-791 | Añadido el martes, 10 de abril de 2018 2:27:36

Chapter
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 52 | posición 790-791 | Añadido el martes, 10 de abril de 2018 2:27:40

Chapter 9. Scoping a Project
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 52 | posición 790 | Añadido el martes, 10 de abril de 2018 2:27:44


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 55 | posición 829-829 | Añadido el miércoles, 11 de abril de 2018 2:01:30

Making the Big Plan
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 55 | posición 831-833 | Añadido el miércoles, 11 de abril de 2018 2:01:50

Break the problem into pieces. Bring the pieces into focus by estimating them. Defer less valuable pieces.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 56 | posición 846-847 | Añadido el miércoles, 11 de abril de 2018 2:06:14

What, Me Worry?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 57 | posición 866-867 | Añadido el miércoles, 11 de abril de 2018 2:09:25

Chapter 10. Release Planning
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 57 | posición 867-868 | Añadido el miércoles, 11 de abril de 2018 2:09:38

In release planning the customer chooses a few months' worth of stories, typically focusing on a public release.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 58 | posición 878-879 | Añadido el miércoles, 11 de abril de 2018 2:10:44

Release planning allocates user stories to releases and iterationswhat
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 58 | posición 883-884 | Añadido el miércoles, 11 de abril de 2018 2:10:53

Who Does Release Planning?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 58 | posición 885-885 | Añadido el miércoles, 11 de abril de 2018 2:11:01

customer and the programmers.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 59 | posición 895-895 | Añadido el miércoles, 11 de abril de 2018 2:11:46

How Stable Is the Release Plan?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 59 | posición 895-897 | Añadido el miércoles, 11 de abril de 2018 2:11:56

Not at all. The only thing we know for certain about a plan is that development won't go according
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 59 | posición 895-897 | Añadido el miércoles, 11 de abril de 2018 2:12:03

Not at all. The only thing we know for certain about a plan is that development won't go according to it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 59 | posición 901-902 | Añadido el miércoles, 11 de abril de 2018 2:12:53

How Far in Advance Do You Plan?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 59 | posición 903-904 | Añadido el miércoles, 11 de abril de 2018 2:13:18

point going into great detail for years into the future. We prefer to plan one or two
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 59 | posición 903-904 | Añadido el miércoles, 11 de abril de 2018 2:13:24

point going into great detail for years into the future. We prefer to plan one or two iterations in advance and one or two releases in advance.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 59 | posición 904-904 | Añadido el miércoles, 11 de abril de 2018 2:13:27

We prefer to plan one or two iterations in advance and one or two releases in advance.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 60 | posición 908-909 | Añadido el miércoles, 11 de abril de 2018 2:13:57

The real decider for how far in advance you should plan is the cost of keeping the plan up-to-date versus the benefit you get when you know that plans are inherently unstable.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 60 | posición 910-911 | Añadido el miércoles, 11 de abril de 2018 2:14:05

How Do You Plan Infrastructure?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 60 | posición 920-920 | Añadido el miércoles, 11 de abril de 2018 2:14:54

evolve the infrastructure as you build the functionality.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 60 | posición 920 | Añadido el miércoles, 11 de abril de 2018 2:15:25

De lo contrario pasaras mucho tiempo con la infraestructura y no tendras nada de funcionalidsd
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 61 | posición 923-923 | Añadido el miércoles, 11 de abril de 2018 2:15:48

How Do You Store the Release Plan?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 61 | posición 924-924 | Añadido el miércoles, 11 de abril de 2018 2:16:01

set of cards. Each card represents a user story
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 61 | posición 933-934 | Añadido el miércoles, 11 de abril de 2018 2:16:59

How Much Can You Put into a Release?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 61 | posición 935-936 | Añadido el miércoles, 11 de abril de 2018 2:17:18

We use the term velocity to represent how much the team can do in an iteration.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 63 | posición 961-962 | Añadido el miércoles, 11 de abril de 2018 2:19:27

Chapter 11. Writing Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 64 | posición 968-968 | Añadido el miércoles, 11 de abril de 2018 2:20:03

user story is a chunk of functionality (some people use the word feature) that is of value to the customer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 64 | posición 973-973 | Añadido el miércoles, 11 de abril de 2018 2:20:38

Principles of Good Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 64 | posición 973 | Añadido el miércoles, 11 de abril de 2018 2:20:42


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 64 | posición 974-974 | Añadido el jueves, 12 de abril de 2018 18:54:24

Stories must be understandable to the customer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 64 | posición 977-977 | Añadido el jueves, 12 de abril de 2018 18:54:29

We like to write user stories on index cards.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 65 | posición 984-984 | Añadido el jueves, 12 de abril de 2018 18:54:36

The shorter the story the better.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 65 | posición 988-988 | Añadido el jueves, 12 de abril de 2018 18:55:10

not that you don't need all of those details. You just don't need them all up front.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 65 | posición 988-988 | Añadido el jueves, 12 de abril de 2018 18:55:17

not that you don't need all of those details. You just don't need them all up front.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 65 | posición 988-988 | Añadido el jueves, 12 de abril de 2018 18:55:21

It's not that you don't need all of those details. You just don't need them all up front.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 66 | posición 999-999 | Añadido el jueves, 12 de abril de 2018 18:56:35

Stories need to be of a size that you can build a few of them in each iteration.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 66 | posición 1002-1003 | Añadido el jueves, 12 de abril de 2018 18:57:14

The customer must write the story; the developers then estimate the story.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 66 | posición 1010-1010 | Añadido el jueves, 12 de abril de 2018 18:58:05

Feedback from Estimation
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 66 | posición 1010 | Añadido el jueves, 12 de abril de 2018 18:58:38


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 67 | posición 1013-1014 | Añadido el viernes, 13 de abril de 2018 1:33:37

It is very common for a user to write a story that cannot be easily estimated.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 67 | posición 1022-1023 | Añadido el viernes, 13 de abril de 2018 1:35:36

estimate the story. Programmers don't need infinite detail in order to estimate; they just need the customer to translate her needs
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 67 | posición 1023-1023 | Añadido el viernes, 13 de abril de 2018 1:35:40

Programmers don't need infinite detail in order to estimate; they just need the customer to translate her needs
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 67 | posición 1023-1024 | Añadido el viernes, 13 de abril de 2018 1:35:44

Programmers don't need infinite detail in order to estimate; they just need the customer to translate her needs into something concrete that they can take action on.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 67 | posición 1025-1025 | Añadido el viernes, 13 de abril de 2018 1:35:52

Prioritizing User Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 67 | posición 1026-1028 | Añadido el viernes, 13 de abril de 2018 1:36:18

wouldn't have written them, now would they? Instead, the customer needs to prepare to answer the question "What would you like us to implement first, and what will we implement later?"
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 67 | posición 1027-1028 | Añadido el viernes, 13 de abril de 2018 1:36:23

the customer needs to prepare to answer the question "What would you like us to implement first, and what will we implement later?"
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 68 | posición 1036-1036 | Añadido el viernes, 13 de abril de 2018 1:37:06

Traceability
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 68 | posición 1037-1037 | Añadido el viernes, 13 de abril de 2018 1:37:25

customer will have to specify acceptance tests
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 68 | posición 1041-1042 | Añadido el viernes, 13 de abril de 2018 1:38:07

the simpler trace between story and the acceptance tests. If the acceptance tests work, we can safely assume that some code exists that maps to the
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 68 | posición 1041-1042 | Añadido el viernes, 13 de abril de 2018 1:38:10

the simpler trace between story and the acceptance tests. If the acceptance tests work, we can safely assume that some code exists that maps to the story. If
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 68 | posición 1042-1042 | Añadido el viernes, 13 de abril de 2018 1:38:17

If the acceptance tests work, we can safely assume that some code exists that maps to the story. If
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 69 | posición 1044-1044 | Añadido el viernes, 13 de abril de 2018 1:38:25

Splitting User Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 70 | posición 1061-1062 | Añadido el viernes, 13 de abril de 2018 1:40:26

User Story Adornments
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 70 | posición 1062-1062 | Añadido el viernes, 13 de abril de 2018 1:41:36

keep our user stories uncluttered.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 70 | posición 1066-1067 | Añadido el viernes, 13 de abril de 2018 1:41:44

The Story Writing Process
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 70 | posición 1070-1071 | Añadido el viernes, 13 de abril de 2018 1:43:23

feeling your way. The process of writing stories is iterative, requiring lots of feedback.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 70 | posición 1071-1071 | Añadido el viernes, 13 de abril de 2018 1:43:28

The process of writing stories is iterative, requiring lots of feedback.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 71 | posición 1082-1083 | Añadido el viernes, 13 de abril de 2018 1:45:20

Don't be too impressed with your stories. Writing the stories is not the point. Communicating is the point.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 71 | posición 1082-1083 | Añadido el viernes, 13 de abril de 2018 1:45:27

Writing the stories is not the point. Communicating is the point.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 71 | posición 1084-1084 | Añadido el viernes, 13 de abril de 2018 1:45:37

When Are You Done Writing Stories?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 71 | posición 1085-1085 | Añadido el viernes, 13 de abril de 2018 1:45:48

Never,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 71 | posición 1088-1090 | Añadido el viernes, 13 de abril de 2018 1:46:29

meaningful choices. Everyone (especially at the beginning of projects) needs to feel heard. If the customer needs to write (quickly write) two years' worth of stories before he feels listened to, so be it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 71 | posición 1089-1090 | Añadido el viernes, 13 de abril de 2018 1:46:36

Everyone (especially at the beginning of projects) needs to feel heard. If the customer needs to write (quickly write) two years' worth of stories before he feels listened to, so be it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 72 | posición 1096-1097 | Añadido el viernes, 13 de abril de 2018 1:47:47

The Disposition of User Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 72 | posición 1097-1098 | Añadido el viernes, 13 de abril de 2018 1:48:17

Once a user story has been implemented and its acceptance tests are running, the story itself serves no further purpose.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 72 | posición 1099-1100 | Añadido el viernes, 13 de abril de 2018 1:48:25

them is probably the best option. Remember that the stories are encoded in far more detail and accuracy in the acceptance tests,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 72 | posición 1099-1100 | Añadido el viernes, 13 de abril de 2018 1:48:29

stories are encoded in far more detail and accuracy in the acceptance tests,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 74 | posición 1135-1135 | Añadido el viernes, 13 de abril de 2018 1:49:28

Chapter 12. Estimation
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 75 | posición 1136-1136 | Añadido el viernes, 13 de abril de 2018 1:49:38

Base your story estimates on a similar story you've already done.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 74 | posición 1135 | Añadido el viernes, 13 de abril de 2018 1:49:43


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 75 | posición 1145-1145 | Añadido el sábado, 28 de abril de 2018 3:12:43

The best guide to estimating the future is to look for something that happened in the
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 75 | posición 1145-1146 | Añadido el sábado, 28 de abril de 2018 3:12:48

The best guide to estimating the future is to look for something that happened in the past that was about the same as the future thing. Then
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 75 | posición 1148-1149 | Añadido el sábado, 28 de abril de 2018 3:12:56

Estimating the Size of a Story
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 76 | posición 1154-1155 | Añadido el sábado, 28 de abril de 2018 3:14:04

It doesn't actually matter what units you express the estimate
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 77 | posición 1173-1173 | Añadido el sábado, 28 de abril de 2018 3:16:07

Estimating How Much You Can Do in an Iteration
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 78 | posición 1195-1196 | Añadido el sábado, 28 de abril de 2018 3:19:20

The Meaning of Ideal Time
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 80 | posición 1227-1227 | Añadido el sábado, 28 de abril de 2018 3:29:09

Improving Your Estimates
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 81 | posición 1233-1234 | Añadido el sábado, 28 de abril de 2018 3:30:29

Chapter 13. Ordering the Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 81 | posición 1233 | Añadido el sábado, 28 de abril de 2018 3:30:36


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 81 | posición 1234-1235 | Añadido el sábado, 28 de abril de 2018 3:30:48

The most important stories to do first are the ones that contain the highest business value.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 82 | posición 1246-1247 | Añadido el miércoles, 2 de mayo de 2018 2:27:46

All of these techniques are pretty much useless on an XP project. They are useless because dependencies between tasks do not figure strongly, because of the emphasis on minimal technical commitment and constant growth in the design.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 82 | posición 1247 | Añadido el miércoles, 2 de mayo de 2018 2:28:20

Las tecnicas de las que abla son las clasicas. Que organiza por dependencias y camino critico
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 83 | posición 1261-1261 | Añadido el miércoles, 2 de mayo de 2018 2:29:57

Business Value
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 83 | posición 1264-1264 | Añadido el miércoles, 2 de mayo de 2018 2:30:24

We want to get a release to the customer as soon as possible. We want this release to be as valuable to the customer as possible.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 83 | posición 1271-1272 | Añadido el miércoles, 2 de mayo de 2018 2:31:23

Determining business value is a decision entirely within the realm of the business people.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 83 | posición 1271-1271 | Añadido el miércoles, 2 de mayo de 2018 2:31:30

a story? The short answer is that we don't; that is, the developers and project managers don't.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 83 | posición 1271-1271 | Añadido el miércoles, 2 de mayo de 2018 2:31:36

the developers and project managers don't.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 84 | posición 1287-1287 | Añadido el miércoles, 2 de mayo de 2018 2:33:11

Technical Risk
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 84 | posición 1287-1289 | Añadido el miércoles, 2 de mayo de 2018 2:34:32

As the developers look at the stories they will inevitably start thinking about how they will build them. As they do this they will run the gamut of feelings, all the way from "no problem" to "can't be done." These feelings are important, because they are the manifestation of where the project could go off the rails.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 85 | posición 1298-1299 | Añadido el miércoles, 2 de mayo de 2018 2:34:41

Negotiating Between the Two
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 85 | posición 1300-1300 | Añadido el miércoles, 2 de mayo de 2018 2:34:55

Programmers want to tackle high-risk stories first, and customers want to tackle high-value stories first.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 85 | posición 1304-1304 | Añadido el miércoles, 2 de mayo de 2018 2:35:49

programmers' task to make the risk visible, not to make the decision for the customer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 86 | posición 1311-1311 | Añadido el miércoles, 2 de mayo de 2018 2:36:34

Example Release Plan
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 90 | posición 1374-1374 | Añadido el miércoles, 2 de mayo de 2018 2:39:45

Chapter 14. Release Planning Events
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 90 | posición 1374 | Añadido el miércoles, 2 de mayo de 2018 2:40:39


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 90 | posición 1380-1380 | Añadido el miércoles, 2 de mayo de 2018 3:01:06

Changing the Priorities of Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 91 | posición 1383-1384 | Añadido el miércoles, 2 de mayo de 2018 3:01:23

Adding a Story
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 91 | posición 1384-1385 | Añadido el miércoles, 2 de mayo de 2018 3:01:37

other methodologies out there, the biggest difference to customers
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 91 | posición 1384-1385 | Añadido el miércoles, 2 de mayo de 2018 3:01:46

other methodologies out there, the biggest difference to customers is that they don't have to commit to a detailed specification of everything they want before development begins.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 91 | posición 1385-1385 | Añadido el miércoles, 2 de mayo de 2018 3:01:51

customers is that they don't have to commit to a detailed specification of everything they want before development begins.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 91 | posición 1392-1393 | Añadido el miércoles, 2 de mayo de 2018 3:02:37

Rebuild the Release Plan
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 92 | posición 1397-1398 | Añadido el miércoles, 2 de mayo de 2018 3:03:11

but if enough of them mount up that you are sure you aren't going to get everything done, it's time to do something about it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 92 | posición 1397-1398 | Añadido el miércoles, 2 de mayo de 2018 3:03:16

you aren't going to get everything done, it's time to do something about it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 92 | posición 1409-1410 | Añadido el miércoles, 2 de mayo de 2018 3:04:24

Chapter 15. The First Plan
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 92 | posición 1410-1411 | Añadido el miércoles, 2 de mayo de 2018 3:04:36

The first plan is the hardest
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 93 | posición 1412-1412 | Añadido el miércoles, 2 de mayo de 2018 3:04:43

Making the First Plan
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 93 | posición 1417-1418 | Añadido el miércoles, 2 de mayo de 2018 3:05:32

and build up the history to make the later plans better. The first plan, however, is always high on expectations and usually low on delivery.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 93 | posición 1418-1418 | Añadido el miércoles, 2 de mayo de 2018 3:05:36

The first plan, however, is always high on expectations and usually low on delivery.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 94 | posición 1439-1440 | Añadido el miércoles, 2 de mayo de 2018 3:08:14

Choosing Your Iteration Length
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 96 | posición 1460-1461 | Añadido el miércoles, 2 de mayo de 2018 3:09:07

working, tested codewhich is hard to fudge. But milestones only occur at the end of an iteration. The longer the iteration, the more risk you run of sliding just a little bit out of control.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 96 | posición 1460-1461 | Añadido el miércoles, 2 de mayo de 2018 3:09:11

But milestones only occur at the end of an iteration. The longer the iteration, the more risk you run of sliding just a little bit out of control.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 96 | posición 1460-1461 | Añadido el miércoles, 2 de mayo de 2018 3:09:14

But milestones only occur at the end of an iteration. The longer the iteration, the more risk you run of sliding just a little bit out of control.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 97 | posición 1473-1473 | Añadido el miércoles, 2 de mayo de 2018 3:10:26

Getting Started
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 97 | posición 1486-1487 | Añadido el miércoles, 2 de mayo de 2018 3:11:30

Chapter 16. Release Planning Variations
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 97 | posición 1488-1488 | Añadido el miércoles, 2 de mayo de 2018 3:11:39

Some local adaptations of the release planning are shorter releases, longer releases, and shorter stories.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 97 | posición 1486 | Añadido el miércoles, 2 de mayo de 2018 3:11:48


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1490-1495 | Añadido el miércoles, 2 de mayo de 2018 18:29:04

encountered. Short Releases Sometimes you can release much more often, maybe every iteration. This can happen for in-house development and also for application service providers where your users are distant but using thin clients and you have close control over the server. Most of this is good news. Each iteration is ready for production, and going into production with each iteration is perfectly feasible. This usually means that you need to have high confidence in your tests and a very automated build process, but if you
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1491-1491 | Añadido el lunes, 7 de mayo de 2018 2:58:09

Short Releases
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1494-1495 | Añadido el lunes, 7 de mayo de 2018 2:59:03

each iteration is perfectly feasible. This usually means that you need to have high confidence in your tests and a very automated build process,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1495-1495 | Añadido el lunes, 7 de mayo de 2018 2:59:08

you need to have high confidence in your tests and a very automated build process,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1496-1496 | Añadido el lunes, 7 de mayo de 2018 2:59:19

With short releases you don't really need any notion of a release at all.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1499-1500 | Añadido el lunes, 7 de mayo de 2018 2:59:51

customer spends so much time choosing features for the short term that she misses important long-term needs.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1499-1499 | Añadido el lunes, 7 de mayo de 2018 2:59:59

lose strategic vision
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1498-1499 | Añadido el lunes, 7 de mayo de 2018 3:00:05

However, there is a danger to never having "a release." The customer may lose strategic vision
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 98 | posición 1499-1499 | Añadido el lunes, 7 de mayo de 2018 3:00:10

customer may lose strategic vision
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 99 | posición 1504-1504 | Añadido el lunes, 7 de mayo de 2018 3:00:46

Long Releases
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 99 | posición 1505-1506 | Añadido el lunes, 7 de mayo de 2018 3:01:22

Our first reaction to this reality is to question it. Maybe there is some way to release more frequently.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 99 | posición 1512-1514 | Añadido el lunes, 7 de mayo de 2018 3:02:17

send intermediate releases to those customers that may be more interested in these versions. Call them service packs or something. That way at least some of your users will use the system in production,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 99 | posición 1514 | Añadido el lunes, 7 de mayo de 2018 3:02:39

Compartir con norbert
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 99 | posición 1517-1517 | Añadido el lunes, 7 de mayo de 2018 3:02:59

Small Stories
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 100 | posición 1519-1519 | Añadido el lunes, 7 de mayo de 2018 3:03:42

customer finer control over the activities of the team,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 101 | posición 1535-1535 | Añadido el lunes, 7 de mayo de 2018 3:04:43

Chapter 17. Iteration Planning
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 101 | posición 1536-1537 | Añadido el lunes, 7 de mayo de 2018 3:04:59

Each iteration is planned by breaking down the stories for that iteration into tasks. Tasks are scheduled by asking programmers to sign up for the tasks they want, then asking them to estimate their tasks, then rebalancing as necessary.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 101 | posición 1538-1538 | Añadido el lunes, 7 de mayo de 2018 3:05:17

The release plan is synchronized to the rhythms of business.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 101 | posición 1539-1539 | Añadido el lunes, 7 de mayo de 2018 3:05:21

that together tell a good story to the market. The iteration plan is synchronized to the rhythms of programming.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 101 | posición 1539-1539 | Añadido el lunes, 7 de mayo de 2018 3:05:25

The iteration plan is synchronized to the rhythms of programming.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 101 | posición 1538-1538 | Añadido el lunes, 7 de mayo de 2018 3:05:37

The release plan is synchronized to the rhythms of business.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 102 | posición 1556-1556 | Añadido el lunes, 7 de mayo de 2018 3:07:29

Never Slip the Date
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 102 | posición 1557-1557 | Añadido el lunes, 7 de mayo de 2018 3:07:38

principles in planning for Extreme Programming is that the dates are hard dates, but scope will vary.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 102 | posición 1557-1557 | Añadido el lunes, 7 de mayo de 2018 3:07:42

dates are hard dates, but scope will vary.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 103 | posición 1574-1574 | Añadido el lunes, 7 de mayo de 2018 3:09:43

Chapter 18. Iteration Planning Meeting
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 104 | posición 1586-1586 | Añadido el lunes, 7 de mayo de 2018 3:11:07

Understanding the Story
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 105 | posición 1598-1599 | Añadido el lunes, 7 de mayo de 2018 3:12:47

facsimile, providing that everyone understands that the narrative is a supplement to conversation not a substitute for it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 105 | posición 1598-1599 | Añadido el lunes, 7 de mayo de 2018 3:12:53

narrative is a supplement to conversation not a substitute for it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 105 | posición 1597-1597 | Añadido el lunes, 7 de mayo de 2018 3:13:04

tests are the best format for corroborating detail.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 105 | posición 1597 | Añadido el lunes, 7 de mayo de 2018 3:13:29

Los tests son lo mejor herramienta para ponerse de acuerdo en los dryalles
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 105 | posición 1601-1601 | Añadido el lunes, 7 de mayo de 2018 3:13:36

Listing the Tasks for an Iteration
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 105 | posición 1602-1604 | Añadido el lunes, 7 de mayo de 2018 3:14:16

to break the story down into a few finer-grained tasks. Each task should be a few ideal days of effort. The tasks are development tasks, so they don't need to make sense to the customer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 105 | posición 1603-1604 | Añadido el lunes, 7 de mayo de 2018 3:14:20

Each task should be a few ideal days of effort. The tasks are development tasks, so they don't need to make sense to the customer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 105 | posición 1605-1606 | Añadido el lunes, 7 de mayo de 2018 3:14:48

You don't need a major design effort here, but you do need just enough to get a good list of tasks.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 105 | posición 1606 | Añadido el lunes, 7 de mayo de 2018 3:15:54

Antes de programar se puede dar un repaso al codigo que habra que modificar. Hacerlo en grupo
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 106 | posición 1616-1617 | Añadido el lunes, 7 de mayo de 2018 3:17:05

you never plan precisely when each task gets done, or in what order the task gets done.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 106 | posición 1618-1618 | Añadido el lunes, 7 de mayo de 2018 3:17:25

As long as the tasks are kept short and you can write tests for them, you'll be fine.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 106 | posición 1619-1620 | Añadido el lunes, 7 de mayo de 2018 3:17:31

Technical Tasks
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 107 | posición 1628-1628 | Añadido el lunes, 7 de mayo de 2018 3:18:34

Measuring the Velocity of a Programmer
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 107 | posición 1638-1638 | Añadido el lunes, 7 de mayo de 2018 3:19:47

Signing Up and Estimating Tasks
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 107 | posición 1640-1641 | Añadido el lunes, 7 de mayo de 2018 3:20:19

The first thing she needs to do is to estimate how long it will take her to do the task.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 108 | posición 1643-1644 | Añadido el lunes, 7 de mayo de 2018 3:21:26

Be wary of using comparable work from another programmer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 108 | posición 1644-1644 | Añadido el lunes, 7 de mayo de 2018 3:21:40

Programmers do not work at the same speed,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 108 | posición 1648-1648 | Añadido el lunes, 7 de mayo de 2018 3:22:17

Programmers should always assume they have a partner when doing a task,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 108 | posición 1650-1651 | Añadido el lunes, 7 de mayo de 2018 3:22:35

Programmers should also assume that they aren't done with a task until they have all the unit tests written and passing.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 108 | posición 1652-1653 | Añadido el lunes, 7 de mayo de 2018 3:23:02

Programmers can sign up for whatever they want to do.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 109 | posición 1659-1660 | Añadido el lunes, 7 de mayo de 2018 3:23:52

Scut Work
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 109 | posición 1660-1661 | Añadido el lunes, 7 de mayo de 2018 3:24:58

Some project managers on hearing about this "signing up" practice fear there'll be some dirty work that doesn't get done.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 109 | posición 1663-1664 | Añadido el lunes, 7 de mayo de 2018 3:25:15

Team members may choose to do a more formal rotation to take turns doing unpopular work.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 109 | posición 1666-1666 | Añadido el lunes, 7 de mayo de 2018 3:25:22

Too Much to Do
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 109 | posición 1671-1672 | Añadido el lunes, 7 de mayo de 2018 3:26:13

Customers can defer a whole story, or they can choose to split a story and defer one of the resulting parts
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 110 | posición 1676-1677 | Añadido el lunes, 7 de mayo de 2018 3:26:50

Too Little to Do
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 110 | posición 1678-1678 | Añadido el lunes, 7 de mayo de 2018 3:27:02

The programmers ask the customer to add some stories.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 112 | posición 1709-1709 | Añadido el lunes, 7 de mayo de 2018 3:27:27

Chapter 19. Tracking an Iteration
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 112 | posición 1709 | Añadido el lunes, 7 de mayo de 2018 3:27:39


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 112 | posición 1713-1714 | Añadido el lunes, 7 de mayo de 2018 12:52:08

The only thing you know about a plan is that things won't go according to it. So you have to monitor the iteration at regular intervals.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 112 | posición 1715-1716 | Añadido el lunes, 7 de mayo de 2018 12:52:22

Iteration Progress Check
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 112 | posición 1717-1718 | Añadido el lunes, 7 de mayo de 2018 12:53:04

or (heaven forbid) writing a report. Instead, the tracker should visit each programmer one at a time.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 112 | posición 1717-1718 | Añadido el lunes, 7 de mayo de 2018 12:53:10

the tracker should visit each programmer one at a time.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 116 | posición 1776-1777 | Añadido el lunes, 7 de mayo de 2018 12:55:50

Falling Behind
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 116 | posición 1777-1777 | Añadido el lunes, 7 de mayo de 2018 12:56:29

Tracking is passive, until you find that something is up.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 116 | posición 1779-1779 | Añadido el lunes, 7 de mayo de 2018 12:56:37

look for someone else with time available who is willing to accept the task.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 117 | posición 1783-1784 | Añadido el lunes, 7 de mayo de 2018 12:57:12

there aren't any great solutions available, you have to go to the customer and tell her the score.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 117 | posición 1783-1784 | Añadido el lunes, 7 de mayo de 2018 12:57:19

there aren't any great solutions available, you have to go to the customer and tell her the score.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 114 | posición 1743-1784 | Añadido el lunes, 7 de mayo de 2018 12:57:42

features and tasks that had been scheduled for that time period. After this kick-off day the tasks were written on posters and hung up on the wall, waiting to be ticked off as they were completed. Throughout the iteration programmers asked the customers for clarification of requirements; at the same time, customers nudged the emerging product this way and that as they saw what they had imagined taking shape. When a pair of developers completed a task, they went to the wall poster and crossed it off, and moved on to the next one. Ideal as that might sound, there was a problem. Notice how the developers weren't crossing off tasks when they were done. They were crossing them off when they thought they were done. The collaboration hadn't been taken far enough. In spite of the close cooperation during development, the programmers were taking that final step, that business decision, by themselves. This had unpleasant consequences. After the task had been crossed off, the customers would look at the feature and say, "That doesn't work quite right. It needs a minor adjustment." With the process unclear about how to go back in a situation like this, the customers would simply log the discrepancy as a bug. As time went by, the bug list grew: incompletions, small deficiencies, and simple misunderstandings were being added to the bug list. Management started pressuring the developers to lower the bug count. Developers resented the pressure because many of the items clearly weren't "bugs"; they were just clarifications or even changes of mind. Customers resented having the overhead of the extra tracking. Everybody knew the root of the problem was a communication issue, not a lack of competency. But how to fix it? We were already in constant communication. Finally the project manager, Vraj Mohan, saw the simple solution: It should be the customer, not the developer, who would cross off tasks at completion. This would force the final collaborative step that had been missing from the process. Once this step was instituted, most of the friction that had been developing melted away. Programmers had a much more confident sense of completionif the customer saw the final piece of work and was satisfied, the developers could be sure that they were finished with the task. Customers still wanted changes in features after completion, but now the changes were viewed as enhancements or additional features that they themselves had generated, rather than as bugs that were the fault of the programmers. Sharing the Glory At the end of each iteration, the whole team would gather round and watch the developers demo the work in which each had been involved in the preceding three weeks. This was partly so that everyone could be kept abreast of the latest developments, and partly as a morale boostit's gratifying for the developer-customer team to show off the work they have done together to the rest of the team. We would walk down the task list, and for each crossed-off task, one of the developers from the pair that had worked on the task would step forward and demo the feature. As each task came up to be demoed, there was often a hesitation as the two developers who had paired on the task decided on who would be the one to demo the feature. At one such point, at the end of the third or fourth iteration, there happened to be a long delay. To end the wait, the customer whose feature it was stepped forward and good-naturedly announced that she herself would demo it instead of waiting for the developers to decide. It was done on the spur of the moment and brought a laugh from the team watching on; but as Rob and Kent thought about what had just happened, they realized that this was an excellent idea. Why not always have customers demo their features? It would ensure without a doubt that customers would keep up with the work being done during the iteration. In front of an audience, everyone wants to be prepared for their "performance," so no customers would want to lose track of what progress had been made on their features. This process has become popular. It encourages the customer to keep in closer contact with the developer pair: We have found that customers are more eager to check in with developers to see new work as soon as possible, which tends to lead to closer matching of the customer's vision with the final product. Falling Behind Tracking is passive, until you find that something is up. Up in this case means the programmer realizes she can't complete all the tasks she signed up for. There are plenty of reasons this can happen, but the most important point is to do something about it. The first reaction is to look for someone else with time available who is willing to accept the task. He should then give his own estimate of how much time is needed to finish the task. If his estimate ends up greater than the time available, the problem hasn't been solved yet. If nobody has enough time to take on the task, then the team needs to figure out what to do about it. It's important to let everyone know about the problem, as someone may have a good solution at hand. This is where the stand-up meeting comes in handy. Often a bit of informal juggling of a couple people's time can overcome the problem. If there aren't any great solutions available, you have to go to the customer and tell her the score.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 116 | posición 1776-1777 | Añadido el lunes, 7 de mayo de 2018 12:58:08

Falling Behind
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 116 | posición 1777-1777 | Añadido el lunes, 7 de mayo de 2018 12:58:17

Tracking is passive, until you find that something is up.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 116 | posición 1779-1779 | Añadido el lunes, 7 de mayo de 2018 12:58:23

look for someone else with time available who is willing to accept the
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 116 | posición 1779-1779 | Añadido el lunes, 7 de mayo de 2018 12:58:29

look for someone else with time available who is willing to accept the task.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 117 | posición 1783-1784 | Añadido el lunes, 7 de mayo de 2018 12:58:37

If there aren't any great solutions available, you have to go to the customer and tell her the score.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 117 | posición 1788-1788 | Añadido el lunes, 7 de mayo de 2018 12:59:10

The key cure to this problem is to get better at estimating, and this can only come with practice and good task records.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 118 | posición 1795-1796 | Añadido el lunes, 7 de mayo de 2018 13:00:01

When a Programmer Has Extra Time
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 118 | posición 1797-1797 | Añadido el lunes, 7 de mayo de 2018 13:00:18

see if the programmer can help others.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 118 | posición 1798-1799 | Añadido el lunes, 7 de mayo de 2018 13:00:33

what can be brought forward, either a full story or part of a story.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 118 | posición 1799-1799 | Añadido el lunes, 7 de mayo de 2018 13:00:57

consider letting him take a break.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 118 | posición 1802-1802 | Añadido el lunes, 7 de mayo de 2018 13:01:03

When Is the Iteration Done?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 118 | posición 1805-1806 | Añadido el lunes, 7 de mayo de 2018 13:01:21

When Is a Story Done?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 118 | posición 1806-1806 | Añadido el lunes, 7 de mayo de 2018 13:01:36

when the function of that story is demonstated to the customer
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 125 | posición 1909-1910 | Añadido el lunes, 7 de mayo de 2018 13:04:20

Chapter 20. Stand-up Meetings
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 125 | posición 1909 | Añadido el lunes, 7 de mayo de 2018 13:04:38


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 125 | posición 1915-1915 | Añadido el sábado, 12 de mayo de 2018 2:09:53

short daily meetings are invaluable for giving everyone an idea of what other people are doing.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 126 | posición 1927-1928 | Añadido el sábado, 12 de mayo de 2018 2:11:30

Chapter 21. Visible Graphs
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 126 | posición 1928-1929 | Añadido el sábado, 12 de mayo de 2018 2:12:17

Anyone should be able to sense the state of the project by looking at a handful of graphs in the team's working area.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 129 | posición 1977-1977 | Añadido el sábado, 12 de mayo de 2018 2:15:57

Choosing Which Graphs to Show
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 130 | posición 1980-1980 | Añadido el sábado, 12 de mayo de 2018 2:16:04

When a graph has done its job, drop it.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 130 | posición 1990-1990 | Añadido el sábado, 12 de mayo de 2018 2:17:10

select the graphs you need and stop producing graphs you don't.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 130 | posición 1993-1994 | Añadido el sábado, 12 de mayo de 2018 2:17:36

Chapter 22. Dealing with Bugs
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 131 | posición 1995-1996 | Añadido el sábado, 12 de mayo de 2018 2:18:25

Schedule bug fixes with stories so the customer can choose between fixing bugs and adding further functionality.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 132 | posición 2021-2021 | Añadido el sábado, 12 de mayo de 2018 2:21:35

Dealing with Production Defects
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 132 | posición 2022-2022 | Añadido el sábado, 12 de mayo de 2018 2:21:46

The most important thing is to remove the emotion. A bug report is a request for a change to the deployed system.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 133 | posición 2035-2035 | Añadido el sábado, 12 de mayo de 2018 2:23:20

Production Support Team
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 133 | posición 2036-2036 | Añadido el sábado, 12 de mayo de 2018 2:24:10

programmers volunteer to focus on fixing bugs. Each programmer spends a couple of iterations in production support,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 133 | posición 2036-2036 | Añadido el sábado, 12 de mayo de 2018 2:24:15

Each programmer spends a couple of iterations in production support,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 134 | posición 2042-2042 | Añadido el sábado, 12 de mayo de 2018 2:24:26

Dealing with Critical Bugs
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 134 | posición 2043-2044 | Añadido el sábado, 12 de mayo de 2018 2:25:17

The difficulty is identifying which things really are critical bugs. Only the customer can make this call.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 134 | posición 2048-2049 | Añadido el sábado, 12 de mayo de 2018 2:25:26

Chapter 23. Changes to the Team
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 134 | posición 2048 | Añadido el sábado, 12 de mayo de 2018 2:25:48


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 134 | posición 2049-2050 | Añadido el jueves, 17 de mayo de 2018 3:39:43

When the team changes, how does that affect your planning?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 134 | posición 2051-2051 | Añadido el jueves, 17 de mayo de 2018 3:39:52

Coming
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 134 | posición 2051-2052 | Añadido el jueves, 17 de mayo de 2018 3:40:48

Give new team members an iteration or two to get acclimated.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2060-2061 | Añadido el jueves, 17 de mayo de 2018 3:40:58

Going
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2061-2061 | Añadido el jueves, 17 de mayo de 2018 3:41:21

one leaves, reduce
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2061-2062 | Añadido el jueves, 17 de mayo de 2018 3:41:26

one leaves, reduce your next iteration by 20 percent.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2061-2062 | Añadido el jueves, 17 de mayo de 2018 3:41:29

If you have five programmers and one leaves, reduce your next iteration by 20 percent.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2061-2062 | Añadido el jueves, 17 de mayo de 2018 3:41:34

If you have five programmers and one leaves, reduce your next iteration by 20 percent.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2063-2063 | Añadido el jueves, 17 de mayo de 2018 3:41:42

Splitting the Team
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 135 | posición 2063 | Añadido el jueves, 17 de mayo de 2018 3:43:14

Tamaño Maximo de equipo de 10
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2067-2067 | Añadido el jueves, 17 de mayo de 2018 3:43:19

Yesterday's Weather will quickly tell you how much cross-team overhead to plan for.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2068-2068 | Añadido el jueves, 17 de mayo de 2018 3:43:25

People Growing
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 135 | posición 2070-2071 | Añadido el jueves, 17 de mayo de 2018 3:44:08

XP isn't executed by Plug Compatible Programming Units. It is executed by people, changing people.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 136 | posición 2072-2072 | Añadido el jueves, 17 de mayo de 2018 3:44:55

what if you put the management tasks on the board alongside the technical tasks
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 136 | posición 2072 | Añadido el jueves, 17 de mayo de 2018 3:45:22

Si todos comparten tareas en el tablon. Unis podran hacer la tareas de otros
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 136 | posición 2076-2077 | Añadido el jueves, 17 de mayo de 2018 3:45:30

Chapter 24. Tools
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 136 | posición 2080-2081 | Añadido el jueves, 17 de mayo de 2018 3:45:59

Stick with simple tools, like pencil, paper, and whiteboard. Communication is more important to success than whizbang.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 136 | posición 2082-2084 | Añadido el jueves, 17 de mayo de 2018 3:46:13

There are two problems to solve in project management: Keeping track of all data Maintaining communication and relationships between people
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 138 | posición 2102-2103 | Añadido el jueves, 17 de mayo de 2018 3:47:43

Chapter 25. Business Contracts
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- El marcador en la página 138 | posición 2102 | Añadido el jueves, 17 de mayo de 2018 3:47:47


==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 138 | posición 2103-2104 | Añadido el viernes, 18 de mayo de 2018 3:27:24

Traditional business relationships require a little tweaking if you're going to plan and execute a project with
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 138 | posición 2103-2104 | Añadido el viernes, 18 de mayo de 2018 3:27:29

Traditional business relationships require a little tweaking if you're going to plan and execute a project with XP.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 138 | posición 2110-2111 | Añadido el viernes, 18 de mayo de 2018 3:31:03

Outsourcing
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 138 | posición 2111-2116 | Añadido el viernes, 18 de mayo de 2018 3:33:15

The typical outsourcing contract fixes three of the four variables:[1] [1] Thanks to Dave Cleal for many of the refinements on negotiable scope contracts. Scope Time Cost
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 139 | posición 2117-2118 | Añadido el viernes, 18 de mayo de 2018 3:33:29

quality is the hardest variable to measure, surprises tend to get absorbed by reducing qualitya
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 139 | posición 2122-2124 | Añadido el viernes, 18 de mayo de 2018 3:33:43

the contract could read, "Supplier will have eight programmers work for Customer for two months for $320,000. Scope will be negotiated every two weeks according to the classic book Planning Extreme Programming."
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 139 | posición 2129-2130 | Añadido el viernes, 18 de mayo de 2018 3:33:49

In-House Development
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 140 | posición 2140-2141 | Añadido el viernes, 18 de mayo de 2018 3:35:39

The biggest problem with in-house projects is finding the customer.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 141 | posición 2148-2149 | Añadido el viernes, 18 de mayo de 2018 3:35:52

If you can't find a single person to act as customer, you will have to have a committee of customers.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 141 | posición 2155-2155 | Añadido el viernes, 18 de mayo de 2018 3:36:30

Shrink-Wrap
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 141 | posición 2156-2157 | Añadido el viernes, 18 de mayo de 2018 3:36:47

How do you plan when you don't have one customer, you have hundreds, thousands, millions and billions and trillions of customers? XP requires the customer to speak with one voice.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 141 | posición 2157-2157 | Añadido el viernes, 18 de mayo de 2018 3:36:53

This role is called "product manager"
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 141 | posición 2162-2162 | Añadido el viernes, 18 de mayo de 2018 3:37:16

The key point is that responsibility for resolving conflicts is shifted away from development.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La nota en la página 141 | posición 2162 | Añadido el viernes, 18 de mayo de 2018 3:37:51

El PM habla con muchos clientes. Negocio. Marketing. Ventas...
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 142 | posición 2167-2167 | Añadido el viernes, 18 de mayo de 2018 3:38:28

Chapter 26. Red Flags
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 142 | posición 2174-2174 | Añadido el viernes, 18 de mayo de 2018 3:39:22

The solutions are all some form of "slow down until you are under control, then speed up again."
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 143 | posición 2179-2180 | Añadido el viernes, 18 de mayo de 2018 3:39:41

Missing Estimates
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 143 | posición 2183-2183 | Añadido el viernes, 18 de mayo de 2018 3:41:04

Are you committing to too much?
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 143 | posición 2185-2185 | Añadido el viernes, 18 de mayo de 2018 3:41:14

they got behind on testing and refactoring
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 143 | posición 2187-2188 | Añadido el viernes, 18 de mayo de 2018 3:41:21

Have you gotten behind on testing and refactoring? If so, you'll see debugging take an increasing percentage of time but an unpredictable percentage.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2194-2194 | Añadido el viernes, 18 de mayo de 2018 3:42:03

Customers Won't Make Decisions
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2201-2201 | Añadido el viernes, 18 de mayo de 2018 3:43:10

out why the customer won't make the decisions. If his priorities are elsewhere, perhaps the whole project doesn't make sense.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2201-2201 | Añadido el viernes, 18 de mayo de 2018 3:43:14

Find out why the customer won't make the decisions. If his priorities are elsewhere, perhaps the whole project doesn't make sense.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2203-2203 | Añadido el viernes, 18 de mayo de 2018 3:43:20

Defect Reports
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2205-2206 | Añadido el viernes, 18 de mayo de 2018 3:43:57

you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2205-2206 | Añadido el viernes, 18 de mayo de 2018 3:44:01

you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2205-2206 | Añadido el viernes, 18 de mayo de 2018 3:44:04

you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2205-2206 | Añadido el viernes, 18 de mayo de 2018 3:44:07

you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2205-2206 | Añadido el viernes, 18 de mayo de 2018 3:44:12

requests aplenty, but the software should work as specified. If you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 144 | posición 2205-2206 | Añadido el viernes, 18 de mayo de 2018 3:44:16

specified. If you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 145 | posición 2209-2210 | Añadido el viernes, 18 de mayo de 2018 3:44:38

Not Going End to End
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 145 | posición 2214-2214 | Añadido el viernes, 18 de mayo de 2018 3:45:08

Failing Builds
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 145 | posición 2215-2216 | Añadido el viernes, 18 de mayo de 2018 3:45:26

make the integration environment match the production environment more closely.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 145 | posición 2217-2218 | Añadido el viernes, 18 de mayo de 2018 3:45:37

Customer Won't Finish
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 145 | posición 2220-2221 | Añadido el viernes, 18 de mayo de 2018 3:46:05

Make three- to four-month release plans that the customer presents to upper management.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 146 | posición 2224-2224 | Añadido el viernes, 18 de mayo de 2018 3:46:28

Chapter 27. Your Own Process
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 146 | posición 2226-2226 | Añadido el viernes, 18 de mayo de 2018 3:46:59

Once you get comfortable with the basic process, you will grow it to fit your situation more precisely.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 146 | posición 2231-2232 | Añadido el viernes, 18 de mayo de 2018 3:48:18

Adopt XP planning "by the book." Run for a couple of iterations. Then look at the problems you
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 146 | posición 2231-2232 | Añadido el viernes, 18 de mayo de 2018 3:48:21

Adopt XP planning "by the book." Run for a couple of iterations. Then look at the problems you are having
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 146 | posición 2231-2232 | Añadido el viernes, 18 de mayo de 2018 3:48:26

Adopt XP planning "by the book." Run for a couple of iterations. Then look at the problems you are having and experiment with each iteration.
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 147 | posición 2240-2241 | Añadido el viernes, 18 de mayo de 2018 3:48:59

The beauty of an iterative process with short iterations and lots of data is that you can perform many more experiments,
==========
Planning Extreme Programming (RuBrd Edition) (Unknown)
- La subrayado en la página 147 | posición 2241-2242 | Añadido el viernes, 18 de mayo de 2018 3:49:04

Take advantage of your data. Play with your process.
==========
