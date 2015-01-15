# Learning JavaScript design patterns, by Addy Osmani

## What is a pattern?

- Patterns are as templates for how you solve problems

## Pattern-ity Testing, proto-patterns & the rule of three

## Structure of a design pattern

## Writing design patterns

- Es muy dificil, por no decir imposible, saber si un determinado código implementa un patrón determinado. Te puede parecer simplemente que sigue buenas prácticas y que quizá sigue unas reglas que se solapan con algún patrón.

## Anti-patterns

Examples of anti-patterns:

1. Defining a large number of variables in the global context
2. Passing strings rather than functions to either `setTimeout` or `setInterval`
3. Modifying the `Object` class prototype
4. Using JavaScript in an inline form
5. The use of `document.write` instead of `document.createElement`

## Categories of design pattersn

- Creational: they focus on handling object creation mechanisms. Constructor, Factory, Abstract, Prototype, Singleton, Builder.
- Structural: they are concerned with object composition and identify relatinoships between different objects. Decorator, Facade, Flyweight, Adapter, Proxy.
- Behavioral: they focus on improving or streamlining the communication between desparate objects. Iterator, Mediator, Observer, Visitor.

## Design pattern categorization

## JavaScript design patterns

### Creational

- It deals with the idea of creating new things, specifically new objects. 3 common ways to create them:

    // 1.
    var newObject = {}; 
    // 2.
    var newObject = Object.create(null);
    // 3.
    var newObject = new Object();

- Four ways to assign keys and values to an object:

    // 1. Dot syntax
    newObject. someKey = 'Hello World' ; // Write properties
    var key = newObject. someKey; // Access properties

    // 2. Square bracket syntax
    newObject[ 'someKey' ] = 'Hello World' ; // Write properties
    var key = newObject[ 'someKey' ]; // Access properties

    // 3. Object.defineProperty
    Object.defineProperty(newObject, "someKey", {
        value: "for more control of the property's behavior",
        writable: true,
        enumerable: true,
        configurable: true
    });

    // 4. Object.defineProperties
    Object.defineProperties(newObject, {
        "someKey": {
            value: "Hello World", 
            writable: true
        }, 
         "anotherKey": {
             value: "Foo bar", 
             writable: false
         }
    });

### Constructor

Are used to create specific types of objects.

**Basic Constructor**

- You have a constructor function simply by prefixing a call to a constructor function with the keyword `new`. The keyword `this` references teh new object that's being created.
- Problems: it makes inheritance difficult, functions are redefined for each new object but they should ideally be shared between all of te instances

**Constructors with prototypes**





