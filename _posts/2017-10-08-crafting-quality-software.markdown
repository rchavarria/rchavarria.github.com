---
title: "Crafting quality software"
date: 2017-10-08 22:39
author: Ruben Chavarria
categories:
- Reseñas
---

##### de Qafoo GmbH

[![Crafting quality software](https://qafoo.com/book/cover.png)][1]

### Por qué lo he leído

Simplemente pasó por mi timeline de twitter, y me pareció interesante porque trata
de escribir código de calidad en PHP. Así que me picó la curiosidad si había algo
de especial por el hecho de estar enfocado en PHP.

<!-- more -->

### De qué trata el libro

Si le tuviera que contar a alguien de qué va el libro, ¿qué le diría?
¿Qué esperaba encontrar yo en él? 

### Conclusiones y valoración

La *review* en sí del libro. ¿Ha sido lo que esperaba? ¿Qué me ha parecido? ¿Lo recomendaría? ¿Me ha gustado el estilo?

### Qué he aprendido

### Frases que me gustaría recordar

> There is no silver bullet and one of the most important skills every developer 
needs to hone is to assess possibilities and to find the best trade-off for 
the current challenge.

> The solution to the mismatch of fast change and clean code is the art of 
refactoring. Automatic testing and continuous refactoring are the key 
methodologies.

> Once the software stabilizes, you should refactor tests from the acceptance-and 
integration-levels towards the unit-test-level.

> The pure existence of the bug shows that there is room for another test.

> Chances that you will get through a large refactoring without being disturbed 
are low

> If your team accepts refactoring as an essential part of every work they 
perform, you will experience how fast your code base will improve at exactly 
the places you work on a lot.

> Don't be discouraged if the first attempts lead to nothing or weird APIs,
remember that refactoring is a constant process and intermediate steps may 
actually make the code worse.

### Recursos relacionados

- Libería [sciencetist]

[1]: https://qafoo.com/book
[sciencetist]: https://github.com/github/scientist

### Notas tomadas

El libro está en inglés, así que las notas que tomé, las ideas que subrayé, 
están en inglés. Normalmente las traduzco, pero me lleva mucho tiempo y no sé
hasta qué punto todo ese tiempo es valioso.

Aquellas ideas más interesantes que he encontrado, están un poco más arriba, y
esas sí que las he traducido. Para el resto de notas tomadas... lo siento, no.

### 2 Clean Code

#### 2.1 Developers Life is a Trade-Off

There is no silver bullet and one of the most important skills every developer 
needs to hone is to assess possibilities and to find the best trade-off for 
the current challenge.

One of the most important tasks of a developer is to make trade-offs.

You need to be able to reflect your decisions and be prepared to revise them.

#### 2.2 Never Use null

Use a so called *null object* if you need a default instance which does nothing.

If a value could not be found do not return `null` but throw an exception.

Nota: bueno, esta idea está en conflicto con otras que dicen que las excepciones
solo deberían lanzarse en casos excepcionales. Por lo general, si algún
caso puede ser comprobado (el fichero existe,...), es preferible no lanzar
ninguna excepción. No se debería controlar el flujo de la aplicación lanzando
o no excepciones. Pero en la práctica, he hecho y me he encontrado de todo. 

#### 2.3 Struct classes in PHP

### 3 Object Oriented Design

#### 3.1 Learn OOD - to unlearn it again

As can be seen in many projects, working at the fast feature pace often led to 
big ball of mud (BBOM) code bases, which reduced the agility of the project 
day by day, eventually leading to the stage where changes are costly and 
developers demanded yet another re-write to free themselves of legacy hell. 

The solution to the mismatch of fast change and clean code is the art of 
refactoring.

Automatic testing and continuous refactoring are the key methodologies

In order to master agility, fast feature pace and high quality code at the 
same time, every developer needs to learn the art of refactoring and automated 
testing.

#### 3.2 Object lifecycle control

#### 3.3 Ducks Do Not Type

Si una clase implementa una interfaz o clase abstracta, no debería añadir
nuevos métodos públicos.

#### 3.4 Abstract Classes vs. Interfaces

#### 3.5 ContainerAware Considered Harmful

#### 3.6 Code Reuse By Inheritance

#### 3.7 Utilize Dynamic Dispatch

*Despacho dinámico* llama a algo parecido a la inyección de dependencias, que
cambia su implementación en tiempo de ejecución.

A `trait` is static dispatch, too. Compara un `trait` con una llamada estática,
porque dice que no puedes cambiarla en tiempo de ejecución, y en parte tiene
razón, pero no lo veo del todo cierto.

#### 3.8 When to Abstract?

Abstraction is a bet on the future development of the software

The circumstances will change, so will the view on the best abstraction change.

Do not abstract before you are sure about the actual requirements and before 
there is a need to do so.

### 4 Testing

#### 4.1 Finding the right Test-Mix

Once the software stabilizes, you should refactor tests from the acceptance-and 
integration-levels towards the unit-test-level.

Unit-tests are necessary to stabilize your code, but when you know the 
requirements are not stable yet, then having too many unit-tests can be 
a burden as well.

TDD is about design and not about unit-testing and 100% coverage.

Using acceptance- and integration-tests is a valid approach for TDD and serves 
well during periods of spikes and frequent requirement changes.

#### 4.2 Mocking with Phake

PHPUnit mocks and Mockery require expectations to be part of the "setup" phase.
This is unfortunate, because mock expectations are much more related to the 
"Verify" phase instead.

They don't explicitly differentiate between methods that are mocked 
(verification) or stubbed (returning results). Phake introduces a differentiation

#### 4.3 Testing Effects of Commands With Phake::capture()

See after the `\Phake::capture($order)` call, the `$order` variable contains the 
argument that was passed to the `OrderRepository` from your code.

#### 4.4 Using Mink in PHPUnit

Mink is well known from the Behat community to facilitate Behaviour-Driven 
Development (BDD),

#### 4.5 Introduction To Page Objects

The Page Objects maps the HTML (or JSON) to an object oriented structure you 
can interact with and assert on.

This already is the nice thing with page objects. The test are readable.

The logic must be implemented in the Page Object. By implementing it in a Page 
Object it is re-usable in other tests

Since end-to-end tests also will always be slow'ish (compared to unit tests) 
we advise to only write those tests for critical parts of your application.

#### 4.6 Database Tests With PHPUnit

All decisions boil down to: More test atomicity leads to longer test runs, and 
we can buy test speed by omitting test atomicity.

##### 4.6.1 Removing Data versus Schema Reset

Resetting the full schema is the cleanest approach, but also takes the most 
time. Resetting a selected number of tables is faster, but also more 
cumbersome and error-prone.

Además, borrar los datos no siempre ocurre, por errores o porque se te olvida
al escribir el test, lo que provoca efectos colaterales.

Except for very small and simple projects it is usually best to initialize 
the database before each test class (no estoy de acuerdo, eso seguro que será
muy lento, y sigues teniendo la posibilidad de los efectos colaterales).

#### 4.7 Database Fixture Setup in PHPUnit

The way you initialise your database fixtures depends on your test schema 
management. We suggest to reset schemas at the begin of each test case and 
creating the data right in the test case.

#### 4.8 Using Traits With PHPUnit

Why would traits ever be considered a code smell? There is no reason for 
dynamic dispatch.

A trait establishes a dependency to another class which is defined by the name 
of the trait. Traits establish a static dependency which is hard to mock and
hard to replace during runtime. But we will never mock our test cases, and 
there are no other options.

En un test probablemente no quiero *dynamic dispatch* porque no hay forma de
pasar parámetros al constructor de un test, por lo que no puedo decirle al test
qué implementación quiero usar.

#### 4.9 Testing the Untestable

```
function file_get_contents($path) {
     if (preg_match('~^https?://~', $path) {
         // Load some fixture here
     }
     // Call the original here
     return \file_get_contents($path);
```

Es posible mockear funciones globales en codigo con namespace. Luego, para 
llamar a la original hay que poner la barra invertida delante

#### 4.10 Outside-In Testing and the Adapter and Facade Patterns

Outside-In testing leads to interfaces that are written from what is useful 
for the client object using them, in contrast to objects that are composed 
of collaborators that already exist.

The technique stays the same: Think in terms of what you want the API to look 
from the outside and invent collaborators that help you think about the 
problem. Then implement them until you get to the "leafs" of the object graph. 
Only the leafs should actually contain code to third party software.

#### 4.11 Behavior Driven Development

#### 4.12 Code Coverage with Behat

There is generally no point in having code coverage for Behat test cases 
because of their nature: The purpose of an acceptance test

There is still a scenario where you want to peek at code coverage of Behat 
tests: When creating them as wide-coverage tests before starting to refactor 
legacy code.

#### 4.13 Testing Micro Services

We moved away from the classical testing approach for our end-to-end tests and 
instead focused on metrics.

In order to perform a system test, we install all micro services into a single 
virtual machine.

Systems with entry points to our application. These "emulation daemons" feed 
the system with randomized but production-like data and actions.

#### 4.14 Five Tips to Improve Your Unit Testing

Be Pragmatic About a "Unit"

Test Where the Logic is

Please do not test these trivials explicitely: getters, setters, constructors

Continuously Refactor Test Code

Never change production and test code at the same time.

Keep test code simple. Simple does not mean dirty, it means easy to read and 
understand.

Fixtures

Custom assertions

Identify the patterns that evolve in your test suite and reduce duplication 
by extracting utilities.

Whenever you encounter a bug in your software, write a test that fails due to 
this bug and fix the bug afterwards. The pure existence of the bug shows that
there is room for another test.

The pure existence of the bug shows that there is room for another test.

### 5 Refactoring

#### 5.1 Loving Legacy Code

The business rules that the application is meant to reflect are already written 
down in code.

#### 5.2 Refactoring with the Advanced Boy Scout Rule

If you managed to fix it, commit and resume your original work.

If you did not manage to resolve the issue within $x (maybe 15-20) minutes:
Revert the refactoring attempt, add a `@refactor` annotation. If there already 
is a @refactor annotation, append a `!` to it. After 1-2 sprints, grep your 
code for `@refactor`

Nota: eso suena mucho a `TODO`, de los que nunca se llegan a hacer. No veo
diferencia entre `TODO` y esa etiqueta de `@refactor`.

#### 5.3 Extended Definition Of Done

Define them as a guide for code reviews which are then part of the "Definition 
Of Done" for the team. This also means that the team gets clear guidelines 
for Code Reviews and the reviewer knows what to look for.

Common rules for code structure and patterns on top of what PSR-2 defines are 
helpful for developers and speed up the development.

#### 5.4 How to Refactor Without Breaking Things

Baby Steps

Chances that you will get through a large refactoring without being disturbed 
are low.

#### 5.5 Getting Rid of static

The original `Cache` class will always be called, thus we will always test the 
`Cache` class together with the `UserService`. This is, by definition, not an Unit 
Test any more.

Step 1: Replaceable Singletons

Why is this still problematic? Global side effects, more complex test setup,
anything messing unnecessarily with the test code can be considered bad.

Bueno, en este punto, casi lo considero al revés. Quiero decir, prefiero
soportar un poco de complejidad en los tests, a costa de tener un código de 
producción más sencillo, que al revés.

Step 2: Service Locator

Step 3: Dependency Injection

Problems with using a Service Locator are: still global side effects, hidden
dependencies

You achieved actually two goals by doing this: make everything testable,
extract application configuration

#### 5.6 Refactoring Should not Only be a Ticket

If your team accepts refactoring as an essential part of every work they 
perform, you will experience how fast your code base will improve at exactly 
the places you work on a lot.

#### 5.7 Extracting Data Objects

Too Many Parameters issues: it is really hard to remember which parameter is at
which position, additional information will require you to add even more
parameters, introducing more mandatory data will even force you to change the
parameter order

Associative Arrays

Is a good idea to replace any associative array structure with a data 
object. They're a really good tool for prototyping

Real pain: no defined way to document array structures so the IDE will not be
able to tell you which fields exist, what their purpose is and what type the
fields expect.

There is a high risk for typos.

People will eventually add whatever they need at a single place

Replace any associative array structure with a data object once the structure 
has stabilized a bit.

Smooth Migration:

1. Create a New Method
2. Dispatch Old Method To New
3. Change Use Case
4. Iterate

#### 5.8 Basic Refactoring Techniques: Extract Method

Just understanding each step helps you selecting the best code blocks for 
refactoring, something that PHPStorm cannot do for you.

As a rule of thumb, code in a method should work on the same level of 
abstraction

Risky Extract Method Checklist

- Arrays are not passed by reference,
- Side effects to instance variables: check this more carefully when your
extracted method is called in a loop
- Variables that are declared before and used after the extracted method

#### 5.9 How to Perform Extract Service Refactoring When You Don't Have Tests

The primary risk of failure is the temptation to do too many steps at the same 
time, delaying the re-execution and verification that the code still works

**Step 1**: Create Class and Copy Method

**Step 2**: Fix Visibility, Namespace, Use and Autoloading

**Step 3**: Check for Instance Variable Usage

Instance variable that is only used in the extracted method itself. You can
copy (don't delete it just yet) the variable to the new service.

Instance variable is another object that is injected into the originals class 
constructor or with setter injection. Copy

Instance variable is used for state that is only read in the new class. Pass it
as a new argument

Instance variable is used for state that is read, changed or both in the new 
class. Pass it to a setter. Retrieve it back with a getter

Don't be discouraged if the first attempts lead to nothing or weird APIs,
remember that refactoring is a constant process and intermediate steps may 
actually make the code worse.

**Step 4**: Use New Class Inline

**Step 5**: Inline Method

**Step 6**: Move Instantiation into Constructor or Setter

**Step 7**: Cleanup Dependency Injection

#### 5.10 How You Can Successfully Ship New Code in a Legacy Codebase

Good strategy for this kind of change is called "Branch By Abstraction".

Introduce an abstraction in your code-base and implement the branching part 
by selecting different implementations of this abstraction at runtime.

**Step 1**: Refactoring The First Client

We create a new API for this. While moving the old code we also create an
abstraction

**Step 2**: Iterate Across Clients

You will have to adapt the Facade and the abstraction during this process.

**Step 3**: Finish The Clients

If the code is working well enough and we do not have to change it often it 
is valid to just keep it there and ignore

**Step 4**: Starting a new Implementation

Por ahora, lo que tenemos es solo la fachada, nada de una nueva implementacion

We have an abstraction which we "just" need to implement. Please do this 
test-driven.

The Verifier knows the legacy Facade and the new code – it also implements the 
abstraction. The Verifier now always calls the Facade wrapping the old code and
the new implementation and compares their output.

Librerias como [sciencetist] ayudan a esto

**Step 5**: Delete the Old Code

#### 5.11 Extracting Value Objects

The code smell that is widespread in every codebase I have ever seen and is called 
"Primitive Obsession".

In our example we are missing a DateRange. It'll allow us to heavily unit-test
business logic related to date ranges.

Refactoring Singleton Usage to get Testable Code

To make this code testable without the singleton, we can use the lazy 
initialization pattern.

Since you would want to use constructor injection for all mandatory 
dependencies you could also introduce an optional constructor argument.

### 6 Architecture

#### 6.1 Why Architecture is Important

There are even studies 2 pointing out the costs of bugs in your architecture. 
If they are discovered late, when the system is already in production, then 
fixing these bugs can amplify the costs hundredfold.

One of the things which are hardest to repair in existing systems are 
inconsistencies of your data.

What are the main points you should check when designing a system architecture?

How can the consistency of data be ensured across multiple systems?

How do we verify that the chosen systems fulfil their requirements? What are 
the technical and operational risks of newly introduced systems? How will 
the system handle latencies and failures of nodes? Is the overall application 
resilient against single node failures or how can this be accomplished?

#### 6.2 Scaling Constraints of Languages

6.2.1 Why PHP?

One reason is LCoDC$SS, the abbreviations which describes the network 
architectural properties of HTTP / REST stands for:

- Layered (L)
- Code on Demand (CoD): rendering does not happen on the server
- Client-Server (CS)
- Cached ($)
- Stateless (S)

PHP handles stateless HTTP requests perfectly.

6.2.2 So, Why Not PHP?

Besides HTTP browsers also speak other protocols like WebSocket, 
bi-directional permanent connections. PHP is not built for this.

6.2.2.1 Node.js

What I like to use Node.js for is quickly developing simple servers.

6.2.3 Summary

Choosing the language (virtual machine) is not just a matter of taste.

- developer experience,
- license costs
- different paradigms

#### 6.3 How To Synchronize a Database With ElasticSearch?

The naive approach of synchronizing both data storages: store 
data in database, then store data in search index

The problem with this approach is, as in any distributed system, that both the 
first and the second write will fail at some point and we end up with data 
inconsistency

6.3.1 Transactions

6.3.2 Changes Feed

Is a better way to implement this, often used in systems where you have one 
primary storage and any number of secondary storages.

In this scenario your primary storage defines the state of your system – it is 
commonly called "Source Of Truth".

What we want to do is passing every change in the database on to the search 
index.

Any other system, like your search index or caches should be updated based on 
the state in the database.

With the last sequence number returned from the target system we can now load 
all or just a batch of changes from our database.

6.3.3 Generating Correct Sequence Numbers

The easiest way to implement this is an additional table

#### 6.4 Common Bottlenecks in Performance Tests

True for optimizations in your PHP code but also for optimizations regarding your 
infrastructure. We should measure before we try to optimize and waste time.

PHP scripts you'd use XDebug and KCacheGrind or something like Tideways

6.4.1 System Test Setup

6.4.2 Stack Analysis

Configurar una herramienta para simular los pasos que un usuario típico haría 
en tu página. Ejecutar esos tests y monitorizar cpu, memoria, red,...

6.4.3 It is Not Always The Database

Edge Side Includes (ESI) We tested a large online shop which used ESI so extensively 
that the application servers running PHP were actually the problem.

Network File System (NFS) locking issues

Broken server configurations

Opcode cache failures

But this is also something you will not notice without putting the system under 
load.

#### 6.5 Embedding REST Entities

6.5.1 Entities

As an example I chose the resources Product and Category from the e-commerce 
domain. Note that here is a list of product items linked from a category.

6.5.2 The Use-Case

API is to retrieve the top 20 products from a category. To retrieve these 
together with product details, a client needs 21 GET requests on the first go.

6.5.3 Resource Embedding with HAL

Hypertext Application Language (HAL): encodes any resource using the 
<resource> tag and has its own <link> tag.

### 7 Workflow

#### 7.1 Coding in Katas

If you want to grow beyond yourself, you need to create an environment for 
your practice where failure is allowed.

The actual result of this work is only a secondary concern, same applies to 
finishing the task. What counts is the actual practice.

The important part is to reflect on what you did:

- How did you approach the problem?
- Where did your approach lead you?
- What were the problems?

#### 7.2 Why you need infrastructure and deployment automation

The amount of time wasted on setup, synchronization and deployment of 
applications is often ignored by teams and managers.

7.2.1 Can you make a build in one step?

An argument for introducing a reliable one-step build is that it can be safely 
triggered by any member of the team and therefore reduces the possibility 
of errors drastically.

7.2.2 Do you make daily builds?

7.2.3 Do you use configuration management tools to automate infrastructure?

Configuration management tools all solve the problem of consistently automating 
the setup of new and old servers.

7.2.4 Is the development setup documented and automated?

7.2.5 Can you rollout and rollback deployments in one step?

Asset compilation and database schema migrations that are backwards and 
forwards compatible.

7.2.6 Can applications be deployed to a new server setup without changes to 
the code?

Hardcoded configuration variables are the problem here.
