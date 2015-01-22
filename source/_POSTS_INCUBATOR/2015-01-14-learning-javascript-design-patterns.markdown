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

Este patrón resuelve el problema de redefinir funciones.

    function Car(model, year, miles) {
        this.model = model;
        this.year = year;
        this.miles = miles;
    }

    // Note here that we are using Object.prototype.newMethod rather than
    // Object.prototype so as to avoid redefining the prototype object
    Car.prototype.toString = function () {
        return this.model + " has done " + this.miles + " miles";
    };

## The singleton pattern

- Traditionally it restricts instantiation of a class to a single object
- In its simplest form it can be an object literal
- You could add your own private members and methods to the singleton by encapsulating variable and function declarations inseide a closure
- Eso puede ser usado para controlar que solo existe una instancia del objeto que se quiere crear

``` javascript
var Singleton = ( function () {
    var instantiated;

    function init() {
        // singleton here
        return {
            publicMethod: function () {
                console. log('hello world' );
            },
            publicProperty: 'test'
        };
    }

    return {
        getInstance: function () {
            if (! instantiated) {
                instantiated = init();
            }
            return instantiated;
        }
    };
})();

// calling public methods is then as easy as:
Singleton. getInstance(). publicMethod();
```

- it's quite useful when exactly one object is needed to coordinate patterns across the system

## The module pattern

- it is used to further emulate the concept of classes in such a away that we're able to include both public/private methods and variables inse a single object, thus shielding particular parts from the global scope, reducing the likelihood of your function names conflicting
with this pattern only a public api is returnd, keeping everything else within the closure private

``` javascript
var testModule = ( function () {
    var counter = 0;
    return {
        incrementCounter: function () {
            return counter++;
        }
    };
})();
// test
testModule. incrementCounter();
``` 

- Disadvantages: you alse cant access private members in methods that are added to the object at a later point. it's not simply not possible to patch privates. instead, one must override all public methods which interact with bth buggy privates

## The observer pattern

- allows and object (known as a subscriber) to watch another object (the publisher)
- subscribers are able to register (subscribe) to receive notifications. publishers broadcasts (publishes) a notification
- **the general idea here is the promotion of the loose coupling**
- advantages: dynamic relationships may exist. this provides a great deal of flexibility
- decoupling applications: por ejemplo, cuando el usuario clica un boton, en lugar de actualizar el UI directamente, el click-handler puede publicar uno/varios evetnos y el UI afecgtado escucharlos (puede haber un UI o varios escuchando)
- decoupling ajax requests: con peticiones ajax, lo mismo. podemos tener un componente que hace la peticion ajax y publica eventos antes y después de la request (con los datos incluso). varios componentes de la aplicación pueden reaccionar de forma distinta a esos eventos

## The mediator pattern

it's a behavioural design pattern that allows us to expose a unified interface through which the fdiffferent parts of a system may communicate. promotes loose coupling by ensuring that instead of modules referring to each other explicitly, their interaction is handled through this central point.
it's essentialy a shared subject in the observer pattern
- perhaps the bigggest downside of using the mediator pattern is that it can introduce a single point of failure

*mediator Vs observer* the mediator pattern centralizes rather than simply just distributing. Es el mediador quien tiene la responsabilidad.

## The prototype pattern

- creates objects based on a template of an existing object through cloning
- `Object.create` creates an object which has a specified prototype and which optionally contains specified properties (por ejemplo: `Object.create(prototype, optionalDescriptorObjects)`

## The command pattern


















