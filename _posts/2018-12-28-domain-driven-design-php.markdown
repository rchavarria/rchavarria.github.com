---
layout: post
title: "Domain-Driven Design in PHP"
date: 2018-12-28 11:22
author: Ruben Chavarria
categories:
- Reseñas
---

##### de Carlos Buenosvinos, Christian Soronellas y Keyvan Akbary

[![Domain-Driven Design in PHP](https://d2sofvawe08yqg.cloudfront.net/ddd-in-php/hero?1549447498)][1]

### Por qué lo he leído

No lo he terminado de leer todavía

### De qué trata el libro

### Conclusiones y valoración

### Qué he aprendido

### Frases que me gustaría recordar

## Notas tomadas

1.1 Why Domain-Driven Design?
1.2 How Domain-Driven Design helps?
Y bounded contexts
1. Ubiquitous Language:
2. Strategic Design: Domain-Driven Design addresses the strategy behind the direction of the business, not just the technical aspects.
3. Tactical Design: Domain-Driven Design provides the tools and the building blocks for iterative software deliverables.
   1.2.1 Ubiquitous Language
   consider a Bounded Context is a conceptual boundary around a system.
   The Ubiquitous Language inside a boundary has a specific contextual meaning. Concepts out of this context can have a different meaning.
   1.3 Should I start considering Domain-Driven Design as an option?
   1.4 Main challenges of applying Domain-Driven Design
   1.5 The business value of using Domain-Driven Design
   1.6 Wrap-up
2. Architectural Styles
   2.1 The Good Old Times
   2.2 Layered Architecture
   2.2.1 Model-View-Controller
   an Application Service and its purpose is to orchestrate and organize the domain behaviour. In other words, the Application services are the ones that make things happen and they are the direct clients of a Domain Model. No other type of object should be able to directly talk to the internal layers of the Model layer.
   the View layer receives an object, often a Data Transfer Object (DTO)
   Why create a DTO instead of giving an instance of the Model to the View layer? The main reason and the short answer is, again, Separation of Concerns.
   In terms of a web application in PHP, the Controller usually comprehends a set of classes, which in order to fulfill their purpose “speak HTTP” . That is, they receive an HTTP request and return an HTTP response.
   El controlador no es solo una clae. O una config
   2.3 Inverting Dependencies. Hexagonal Architecture
   As the Domain Model layer depends on concrete infrastructure implementa- tions, the Dependency Inversion Principle⁷ could be applied by relocating the Infrastructure layer on top of the other three layers.
   the Infrastructure layer which can be referred to as low level modules now depend on the UI, the Application Layer and the Domain Layer, which are the high level modules. The dependency has been inverted.
   what is Hexagonal Architecture?, and how does it fit within of all this?
   In terms of the DIP, the Port would be a high level module and an Adapter would be a low level module.
   2.4 Command Query Responsibility Segregation
   CQRS seeks an even more aggressive separation of concerns splitting the Model in two: • The Write Model: Also known as the Command Model, it performs the writes and takes responsibility for the true domain behaviour. • The Read Model: It takes responsibility of the reads within the application and treats them as something that should be out of the Domain Model.
   This strict separation triggers another problem, Eventual Consistency.
   there should be a process that updates the cache system. Cache systems are eventually consistent.
   This kind of processes, speaking in CQRS terminology, are called Write Model Projections or just Projections.
   This process can be synchronous or asynchronous, depending on your needs, and it can be done thanks to another useful tactical design pattern that will be explained in detail later on in the book, Domain Events.
   2.4.1 The Write Model

true holder of domain behaviour.
Post model, leaving it only with command methods. This means we will effectively get rid of all the getter methods
domain events will be published in order to be able to trigger write model projections by subscribing to them.
2.4.2 The Read Model
the read model should be completely disposable
can be removed and recreated when needed using write model projections.
2.4.3 Synchronizing the Write Model with the Read Model
For each type of domain event captured, a specific projection will be executed.
2.5 Event Sourcing

## Recursos

- [Domain-Driven Design in PHP][1], de Carlos Buenosvinos, Christian Soronellas y Keyvan Akbary

[1]: https://leanpub.com/ddd-in-php
