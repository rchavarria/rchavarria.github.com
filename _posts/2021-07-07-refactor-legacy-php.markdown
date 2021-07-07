---
layout: post
title: "Refactor legacy PHP"
date: 2019-03-07 19:39
author: Ruben Chavarria
categories:
- Reseñas
---

##### de Glenn Livingston

[![Refactor legacy PHP](https://images-eu.ssl-images-amazon.com/images/I/51X2%2BpB1gHL.jpg)][1]

### Por qué lo he leído

<!-- more -->

### De qué trata el libro

### Conclusiones y valoración

### Qué he aprendido

### Frases que me gustaría recordar

> Si cada vez que te levantas de una caída, te estás haciendo cada vez
más fuerte

<!-- -->

### Recursos relacionados

- [Refactor legacy PHP][1], de Glenn Livingston

## Notas tomadas

1. Legacy Applications
   In its simplest definition, a “legacy application” is any application that you, as a developer, inherit from someone else.
   The Typical PHP Application
   they are often a series of page scripts, placed directly in the web server document root, to which clients can browse directly.
   There are include files for common configurations and settings, headers and footers, common forms
   Legacy applications will use individual “page scripts” as the access point for public behavior.
   Rewrite or Refactor?
   The Pros and Cons of Rewriting
   Because the existing application can serve as a reference implementation, they feel confident that there will be little or no trial-and-error work in rewriting the application.
   Fred Brooks calls the urge to do a complete rewrite “the second-system effect.”
   The general tendency is to over-design
   Why Don’t Rewrites Work?
   developers who will have to do both maintenance on the existing program and write the completely new version
   The Context-switching Problem
   The Knowledge Problem
   If we put the new developers on the rewrite project, they won’t know enough about the existing system,
   They will have to be trained on these things, most likely by the existing developers.
   linear increase in resources results in a less-than-linear increase in productivity:
   The Schedule Problem

dedicate all the existing developers on the rewrite,
overestimate their own ability to perform a full rewrite and underestimate the amount of time needed to complete it.
the result will be a codebase that is just as bad as the first one, only in different ways.
Iterative Refactoring
quality of the program is improved in small steps, without changing the functionality of the program.
A refactoring approach is decidedly less appealing than a complete rewrite. It defies the core sensibilities of most developers. The developers have to continue working with the system as it is,
the goal of any single refactoring step is not “perfection”. The goal in each step is merely “improvement”.
Legacy Frameworks
Framework-based Legacy Applications
Refactoring To A Framework
My experience with legacy PHP applications has been that they are almost as resistant to framework integration as they are to unit testing.
If the application was already in a state where its logic could be ported to a framework, there would be little need to port it in the first place.
Review and Next Steps
2. Prerequisites
   A revision control system A PHP version of 5.0 or higher An editor or IDE with multi-file search-and-replace A style guide of some sort A test suite
   Revision Control
   PHP Version
   PHP 5.0 is the bare minimum, because that was when class autoloading became available, and we depend on autoloading as one of our very first improvements.
   Editor/IDE
   Style Guide
   modifying the existing style, no matter how ugly or inconsistent it is, can give rise to subtle bugs and behavioral changes from something as simple as adding or removing braces in a conditional.
   I suggest that the only reason to modify the existing style is when it is inconsistent within an individual file.
   If you decide to reformat, do so only as you move bits of code from one file to another, or as you move files
   No lo modifiques en gran numero de ficheros o sera un infirno. Mejor poco a poco y con cambios controlados
   Test Suite
   The key here is not to test what the system units ought to do, but what the system as a whole already does.
   The criteria for a successful test is that the system generates the same output after a change as it did before that change. This kind of test is called a characterization test
   En un sistema legacy. Posible.ente no hay rests y las unidadrs a yestear no sean facilmenge identificabkes  . Sera mas facil hacer otro tipo de test. Nada de test unitario

Review and Next Steps
3. Implement An Autoloader
   PSR-0
   PSR-0 is a PHP Framework Interoperability Group recommendation for structuring your class files.
   We use PSR-0 instead of the newer PSR-4 recommendation because we are dealing with legacy code,
   Under PSR-0, the
   the fully-qualified class name \Foo\Bar\Baz_Dib would be found in a sub-path named Foo/Bar/Baz/Dib.php
   A Single Location For Classes
   Before we implement a PSR-0 autoloader, we need to pick a directory location in the codebase to hold every class
   This directory will be the central location for all classes used throughout the project.
   Add Autoloader Code
   register it with spl_autoload_register()
   As A Global Function

Al fi nal. El autoloader lo que hace es un require
classes
Practicamente igual que la function global
As A Closure
As A Static or Instance Method
preferred way of setting up an autoloader.
Using The __autoload() Function
under PHP 5.0
under PHP 5.0 it is our only alternative.
Autoloader Priority
we need it to be available before any classes get called in the codebase.
Common Questions
What Are The Performance Implications Of Autoloading?

evidence is mixed and situation-dependent.
Any performance drag incurred from autoloading is minuscule compared to the other possible performance issues in your legacy application,
How Do Class Names Map To File Names?
Review and Next Steps
4. Consolidate Classes and Functions
   autoloader in place, we can begin to remove all the include calls that only load up class and function definitions.
   When we are done, the only remaining include calls will be those that are executing logic.
   Consolidate Class Files
   Find an include statement that pulls in a class definition file.
   Move that class definition
   matching the PSR-0 rules.
   remove that include statement.
   make sure that all the files now autoload that class
   Repeat until there are no more include
   Consolidate Functions Into Class Files
   autoloading only works for classes.
   The solution here is to move the functions into class files, and call the functions as static methods on those classes.
   process we will follow:
   Find an include statement that pulls in a function
   Convert that function definition file into a class file of static methods;
   change calls to those functions into static method calls.
   Testear. Probar en produccion. Porque no trnelos tests
   Spot check
   Autoload
   Move the class file
   remove the relevant include statement.
   Spot check again
   Commit, push, and notify QA.
   Repeat
   Common Questions
   leave the autoloader include in place as part of our bootstrapping or setup code.
   There is, of course, a performance reduction in loading two files instead of one. The question is how much of a reduction, and compared to what?
   The class should be loadable without side effects, and the other logic should be executable without having to load the class.

I recommend instance methods over static ones. Among other things, it gives us a constructor method that can be called on instantiation, and it makes testing easier in many cases.
It would be great if there was some way to automate the process to make it both faster and more reliable. Unfortunately, I have not yet discovered any tools that make this process easier. As far as I can tell, this kind of refactoring is still best done “by hand” with strong attention to detail.
5. Replace global With Dependency Injection
   Dependency injection turns out to be very straightforward as a concept, but is sometimes difficult to adhere to as a discipline.
   Global Dependencies
   global keyword, and realize they can create the connection once in a setup file, then pull it in from the global scope:
   Esta key word parece mas eligrosa que las variables globakes. Puedes hacer global practicamenge  ualqiyr cosa
   The Replacement Process
   Find a global variable in one of our classes.
   Move all global variables in that class to the constructor and retain their values as properties, and use the properties instead of the globals.
   Spot check that the class still works.
   Convert the global calls in the constructor to constructor parameters.
   Convert all instantiations of the class to pass the dependencies.
   Spot check, commit, push, and notify QA.
   Repeat with the next global call in our class files, until none remain.
   Common Questions


What About Class Names In Variables?
$record = new $class;
The best we can do is to search for new\s+\$ without any class name, and modify the calls individually by hand.
What About Superglobals?
(although we can search for them by name). Because they truly are global, we need to remove them from our classes just as much as we need to remove the global keyword.
Because they truly are global, we need to remove them from our classes just as much as we need to remove the global keyword.
As a solution, we can use a Request data structure class. The Request encapsulates a copy of each of the non-$_SESSION superglobals.
// ... 3 $request = new \Mlaphp\Request($GLOBALS);
Modifications to the values in one Request object will not be reflected in a different Request object,
Review and Next Steps
Replace new With Dependency Injection

The point of dependency injection is to push the dependencies in from the outside, thereby revealing the dependencies in our classes.
One of the keys to dependency injection is that an object may either create other objects, or it may operate on other objects, but not both.
The Replacement Process
Find a class with the new keyword in it.
For each one-time creation in the class … Extract each instantiation to a constructor parameter.
For each repeated creation in the class … Extract each block of creation code to a new Factory class. Create a constructor parameter for each Factory
Usa factories para los casos en ls que se crean mumltiples objetos de la misma clase. En un bucle por cierto
We have two kinds of creation to look for: “one-time” and “repeated.”
Common Questions
What About Exceptions and SPL Classes?
there are two reasonable exceptions to this rule: Exception classes themselves, and certain built-in PHP classes, such as the SPL classes.
when in doubt, err on the side of dependency injection.
Ante la duda. Tira hacia el lado de la inyecciln dependencias
What About Intermediary Dependencies?
Isn’t This A Lot Of Code?
The real issue here, though, is not “more code.” The issues are “more testable,” “more clear,” and “more decoupled.”
how can we tell what ItemsGateway needs to operate? What other parts of the system will it affect?
Should A Factory Create Collections?
The key is to keep object creation (and related operations) separate from object manipulation.
Can We Automate All These Injections?
Yes, there is. It is called a Container.
Using a Container brings distinct advantages:
Container for a database connection; the connection is created once and then reused over and over again.
We can put complex object creation
has disadvantages as well:
We have to drastically change how we think about our object creation,
fancy new toy that has many of the same problems as global.
We will add one eventually, but it will be as the very last step of our modernization process.
7. Write Tests
   Fighting Test Resistance
   if we do not write tests, we are condemning ourselves to continued rounds of suffering later.
   So while it may be true that “writing tests” sucks, it is also true that “having written tests” is awesome.
   The Way Of Testivus
   The core message of The Way of Testivus is “More testing karma, less testing dogma.”
   We should not get hung up on writing “proper” unit tests that adhere to every commandment of testing dogma. Instead, we should write the best test we can, even if the test is imperfect:
   Setting Up A Test Suite
   Install PHPUnit
8. Extract SQL Statements To Gateways

the principles apply to any form of data storage.
No.sql  escribir ficheros. Llamr a servicios...
Embedded SQL Statements
replace the embedded SQL logic with calls to our SQL-related class methods. We will do this by creating a series of Gateway classes. The only thing these Gateway classes will do is get data from, and send data back to, our data sources.
The Extraction Process
In general, this is the process we will follow: Search the entire codebase for SQL statements.
move the statement and relevant logic to a related Gateway class method.
Write a test for the new Gateway method.
Replace the statement and relevant logic in the original file with a call to the Gateway class method.
Search for SQL Statements
Move SQL To A Gateway Class
The task of extracting the SQL to a Gateway is detail-oriented and context-specific.
Vamos. Que depende de cada caso
To determine our namespace and class names, the first thing we need to decide is whether to organize by “layer” or by “entity.”
layers,
This naming arrangement structures the classes by their operational purpose in the codebase.
by domain entities,
This naming arrangement structures the classes by their purpose within the business logic domain.
I recommend organizing by domain entities.
get() the data, find() the data, fetch() the data, select()
Method Names
get() the data, find() the data, fetch() the data, select()
We should stick with any existing naming convention as much as possible.
While the method name itself does not matter, consistency-of-naming does.
When we create our Gateway methods, we should never assume the parameter values are safe.
best solution is to use prepared statements and parameter binding
Write A Test
Replace The Original Code
Common Questions
What About Repetitive SQL Strings?
Dependera del caso. Pero habra que añadir metodos o añadir parametros a metodos existentes
What About Complex Query Strings?
The main considerations are to determine which variables are used in the query-building logic, and to set those up as parameters to our new Gateway method.
What about Queries inside non-Gateway classes?
What About Multiple Queries And Complex Result Structures?
identify how we can split up the queries into Gateway methods.
determine which Gateway class should receive the extracted logic.
we have to choose which is the “primary” subject of the query.
What If There Is No Database Class?
Calls to mysql functions
If we can upgrade to PDO, we should.
I suggest we wrap the mysql calls in a class that proxies method calls to the mysql functions.
Review and Next Steps
9. Extract Domain Logic To Transactions

Embedded Domain Logic
Although we have extracted SQL statements, the page scripts and classes are probably manipulating the results and performing other actions
These manipulations and actions are the core of the domain logic,
Domain Logic Patterns
Martin Fowler’s Patterns of Enterprise Application Architecture (PoEAA) catalogs four domain logic patterns:
Transaction Script “… organizes [domain] logic primarily as a single procedure,
Domain Model “… creates a web of interconnected objects,
order form.” Table Module “… organizes domain logic with one class per table in the database,
Table Module “… organizes domain logic with one class per table in the database,
Service Layer
I strongly recommend purchasing PoEAA in hard copy and reading the pattern descriptions and examples in full.
we will begin by using the Transaction Script pattern when we extract our domain logic.
De los cuatro patroneds. El mas probable es este
we extract the domain logic from the page script and dump it into a class method mostly intact.
one of our goals here is to avoid changing the existing logic too dramatically.
We are refactoring, not rewriting.
The Extraction Process
Search the entire codebase for uses of Gateway classes that exist outside Transactions classes.
surrounding the Gateway operations to discover which portions of that logic are related to the domain behaviors of the application.
discover which portions of that logic are related to the domain behaviors of the application.
Extract the relevant domain logic to one or more Transactions classes
Search For Uses Of Gateway
where the Gateway is used. The code surrounding that usage will be our candidate for extracting domain logic.
Discover And Extract Relevant Domain Logic
normalizing, filtering, sanitizing, and validating of data
these and other operations:
normalizing, filtering, sanitizing, and validating of data
calculation, modification, creation, and manipulation of data
sequential or concurrent operations and actions using the data
retention of success/failure/warning/notice messages
retention of values and variables for later inputs and outputs
Example Extraction

We named the ArticleTransactions methods for the domain logic being performed, not for the implemenation of the underlying technical operations.
Transactions class as properties. The code in the original page script has been greatly reduced.
The code in the original page script has been greatly reduced.
It is now essentially an object creation and injection mechanism, passing user inputs to the domain layer and getting back data to output later.
Spot Check The Remaining Original Code
Transactions from the original code, we need to make sure the original code works when using the Transactions
make sure the original code works when using the Transactions
Write Tests For The Extracted Transactions
Spot
Spot Check Again, Commit, Push, Notify QA
We continue extracting and testing until all Gateway calls occur inside Transactions classes.
Common Questions
Are We Talking About SQL Transactions?
The term “Transaction Script” refers to an architectural pattern,
One useful rule-of-thumb is that pieces of domain logic should be split up according to how well they would fit inside a single SQL transaction.
What About Repeated Domain Logic?
Are the pieces of logic similar enough to be combined into a single method, or must they be different methods (or even in completely different Transactions) ?
Are Printing And Echoing Part Of Domain Logic?
Our Transactions classes should not be using print or echo. The domain logic should only return or retain data.
Can A Transaction Be A Class Instead Of A Method?
some transactions may be complex enough that they truly require their own separate classes.
What About Domain Logic In Gateway Classes?
we should probably extract it to our Transactions
What About Domain Logic Embedded In Non-Domain Classes?
it may be wise to move the class into the domain namespace.
If the class can reasonably be considered part of the domain,
it may be wise to move
Review and Next Steps
10. Extract Presentation Logic To View Files

we will separate all of our presentation logic to its own layer so we can test it separately from our business logic.
Embedded Presentation Logic
echo and print but also header() and setcookie(). Each of these generates some form of output.
Eso estaria considerado presentation logic
The script should first perform all of the business logic, then pass the results over to the presentation logic.
we will move toward using a Response object in our page scripts
The Extraction Process
Find a page script that contains presentation logic mixed in with the rest of the code.
rearrange the code to collect all presentation logic into a single block after all the other logic in the file,
Extract the block of presentation logic to a view file to
Add proper escaping to the presentation logic
Search For Embedded Presentation Logic
search facility to find all occurrences of echo, print, printf, header, setcookie, and setrawcookie.
Rearrange The Page Script and Spot Check
Working line-by-line and block-by-block, we move all presentation logic to the end of the file
moved variables not used by the business logic, such as $current_page, down the presentation block
moved the header.php include down to the presentation block
moved the header.php include down to the presentation block moved logic and conditions acting only on presentation variables,
When creating the presentation block, we should be careful to follow all the lessons we learned from earlier chapters about dependency injection.
Among other things, this means no use of globals, superglobals, or the new keyword.
Extract Presentation To View File and Spot Check
Create a views/ Directory
Pick A View File Name
Move Presentation Block To View File
paste it into our new view file as-is.
original presentation block in the page script, we create a Response object in our page script and point it to our view file with setView(). We also set up an empty call to setVars() for later, and finally call the send() method.
create a Response object in our page script and point it to our view file with setView(). We also set up an empty call to setVars() for later, and finally call the send() method.
Add Proper Escaping
The defense against XSS is to escape all variables all the time
If we remember one thing about escaping output, it should be the htmlspecialchars() function.
Write View File Tests
Calling requireView() invokes the view file but returns the results instead of generating output.
Now we need our test to look at the output to see if it is correct.
Common Questions
What About Headers And Cookies?
Dealing with these output methods can be problematic.
Response object really helps us. The class comes with methods that buffer the header() and related native PHP functions, but do not call those functions until send() time.
What If We Already Have A Template System?
keep using the existing template system
it will be important that we have a single way of interacting with the presentation layer in our page scripts.
We should not use the template system in some page scripts and the Response object in others.
What About Streaming Content?
What If We Have Lots Of Presentation Variables?
One solution is to collect commonly-used variables into one or more objects of their own.
What About Class Methods That Generate Output?
it may be the case that domain classes or other support classes use echo or header() to generate output.
we need to find a way to remove these calls without breaking our legacy application.
convert each use of echo, print, and so on to a return.
What About Business Logic Mixed Into The Presentation?
extract an equivalent set of business logic calls from the presentation logic, capture the results to a variable, and then pass that variable to the presentation.
What If A Page Contains Only Presentation Logic?
even these page scripts should be converted to use a Response and a view
even these page scripts should be converted to use a Response and a view file. A
11. Extract Action Logic To Controllers

“model” domain logic
“view” presentation logic.
dependency logic, which uses the application settings to create objects
action logic (sometimes called business logic) which uses those objects to perform the page actions
Embedded
Embedded
Embedded Action Logic
We must extract the action code to a class of its own to separate the various remaining concerns of our page script.
The Extraction Process
the main issue will be picking apart the dependency setup portions from the action logic itself.
process is as follows:
Find a page script where action logic is still mixed in with the rest of the code.
rearrange the code so that all action logic is in its own central block.
Extract the central block of action logic to a new Controller class,
unit test for the new Controller
Search For Embedded Action Logic
Rearrange The Page Script
Rearrange The Page Script and Spot Check
rearrange the code so that all setup and dependency-creation work is at the top, all the action logic is in the middle, and the $response->send() call is at the bottom.
The code in the dependency block should only create objects, and the code in the controller block should only operate on objects that have been created in the dependency block.
Extract A Controller Class
We add two empty methods as placeholders for later: the __invoke() method will receive the action logic from the page script, and the constructor
we cut the controller block from the page script, and paste it into the __invoke() method as-is.
Once we have a working block of action logic in the __invoke() method, we will convert the method parameters into constructor parameters so that the Controller can use dependency injection.
Write A Controller
Write A Controller Test
Common Questions

Can We
Can We Pass
Can We Pass Parameters To The Controller Method?
In general, we should avoid doing
In general, we should avoid doing so at
we need a very high level of consistency in our controller invocations for a later modernization step.
Can A Controller Have Multiple Actions?
Our first pass at extracting action logic from the page script should keep the code pretty much intact,
Once the code is in the class, though, it is perfectly reasonable to split the logic
What If The Controller Contains include Calls?
We want to encapsulate action logic in classes, not in files that execute behavior the moment we include them.
For now,
include calls in the controller block of our page scripts are ugly but necessary
Review and Next Steps
We now have a full Model View Controller system in place: a domain layer for models, a presentation layer for views, and a controller layer that connects the two.
12. Replace Includes In Classes

we will need to replace include calls with method calls
Embedded include Calls
We want to decouple this logic so that the logic in the include file does not intrude on the scope of the class methods in which is it used.
We do this by extracting the logic of the include file to a class of its own.
The Replacement Process
the process is as follows:
Search the classes/ directory for an include call in a class.
search the entire codebase to find how many times the included file is used.
Refactor the copied code so that it follows all our existing rules: no globals, no new, inject dependencies, return instead of output, and no include calls.
Esto es mas o menos el resumen deel libro... Si ludo lo pudiera leer
Copy the contents of the included file as-is to a new class method.
Replace the discovered include call with inline instantiation of the new class and invocation of the new method.
coupled variables; add these to the new method signature by reference.
Delete the original include file;
Write a unit test for the new class, and refactor the new class so that it follows all our existing rules:
Finally, replace each inline instantiation of the new class in each of our class files with dependency injection,
Search For include Calls
Replacing A Single include Call
copy the entire contents of the include
paste the entire contents of the include file in its place.
Replacing Multiple include Calls
Copy include File To Class Method
Replace The Original include Call
Discover Coupled Variables Through Testing
We need to pass into the new class method all the variables it needs for execution, and to make its variables available to the calling code when the method is done.
Replace Other include Calls And Test
Delete The include File And Test
Write A Test And Refactor
Convert To Dependency Injection and Test
Commit, Push, Notify QA
Common Questions

Can One Class Receive Logic From Many include Files?
it may be reasonable to collect them into the same class, each with their own method name.
What About include Calls Originating In Non-Class Files?
Our main goal here is to remove include calls from class files, not necessarily from the entire legacy application.
it is likely that most or all include calls outside our classes are part of the presentation logic
13. Separate Public And Non-Public Resources
    we need special protections on resources we intend to keep private,
    we need to rely on obscurity to make sure that clients do not browse to resources not intended to be public.
    Intermingled Resources
    our web server acts as a combined front controller, router, and dispatcher for our legacy application.
    our web server acts as a combined front controller, router, and dispatcher for our legacy application. The routes to the page scripts are mapped directly onto the file system,
    our web server acts as a combined front controller, router,
    our web server acts as a combined front controller, router, and dispatcher for our legacy application.
    The routes to the page scripts are mapped directly onto the file system,
    there are large parts of our application that we do not want to be directly accessible by outsiders.
    For example, directories related to configuration
    The Separation Process
    It affects the server configuration as well as the legacy application structure.
    the process is as follows:
    Create a new document root directory in our legacy application, along with a temporary index file.
    Create a new document root directory in our legacy application, along with a temporary index file. Reconfigure the server to point to the new document root directory,
    Create a new document root directory in our legacy application,
    Create a new document root directory in our legacy application, along with a temporary index file.
    server to point to the new document root directory,
    Remove the temporary index file, then move all public resources to the new document root,
    move all public resources to the new document root,
    Create A Document Root Directory
    add a new docroot/ directory at the top level of the application.
    Reconfigure The Server
    point to the new docroot/ directory.
    Move Public Resources
    all of our page scripts, style sheets, JavaScript files, images, and so on. It does not include anything that users should not be able to browse to: classes, includes, setup, configuration, command-line scripts, tests, view files, and so forth.
    Commit, Push, Coordinate
    Common Questions
    Is This Really Necessary?
14. Decouple URL Paths From File Paths
    Coupled Paths
    problems.
    if we want to expose a new or different URL, we have to modify the location
    we cannot change what page script responds to a particular URL.
    There is no way intercept the incoming request before it is routed.
    The Decoupling Process
    we will have to make a change to our web server configuration. Specifically, we will enable URL rewriting so we can point all incoming requests to a front controller.
    The process, in general, is as follows:
    Create a front controller script in the document root.
    Create a pages/ directory for our page scripts, along with a “page not found” page script and controller.
    Reconfigure the web server to enable URL rewriting.
    Spot check
    Move all page scripts from docroot/ to pages/, spot checking along the way.
    Commit, push, and coordinate
    Add A Front Controller

add a front controller script.
We will also add a “page not found” script, controller, and view.
It uses a Router class to map the incoming URL to a page script.
Create A pages/ Directory
we will move all our page scripts out of the document root and into this new directory.
Reconfigure The Server
enable URL rewriting.
Once URL rewriting is enabled, we need to instruct the web server to point all incoming requests to our front controller.
instruct the web server to point all incoming requests to our front controller.
Spot Check
Move Page Scripts
move all of our pages scripts out of docroot/ and into our new pages/ directory.
Commit, Push, Coordinate
Common Questions
Did We Really Decouple The Paths?
Yes, we have achieved our decoupling goal. This is because we now have an interception point between
Using the Router, we could create an array of routes
15. Remove Repeated Logic In Page Scripts
    They all look very similar. Each one loads a setup script, instantiates a series of dependencies for a page controller, invokes that controller, and sends the response.
    Repeated Logic
    The Removal Provess
    process is as follows:
    Modify the front controller to add setup, controller invocation, and response sending.
    Modify each page script to remove the setup, controller invocation, and response sending.
    Spot check, commit, push, and notify QA.
    Modify The Front Controller
    Remove Logic From Page Scripts
    we have added setup, controller invocation, and response-sending work to the front controller, we can remove that same work from each page script.
    Spot Check, Commit, Push, Notify QA
    Common Questions
    What If The Setup Work Is Inconsistent?
    page script, we have a problem to deal with. If the page scripts do not enjoy an indentical setup process at this point, we should do what we can to address that before continuing.
    If the page scripts do not enjoy an indentical setup process at this point, we should do what we can to address that before continuing.
16. Add A Dependency Injection Container

What Is A Dependency Injection Container?
the idea behind dependency injection is that we push depependencies into an object from the outside.
This creation process has sometimes been deeply layered, as when the dependencies have dependencies.
Regardless of the complexity and depth, the logic for doing so is currently embedded in page scripts.
The idea behind a dependency injection container is to keep all that object creation logic in a single place,
When the container is inside an object, and that object uses it to retrieve dependencies, we are only one step removed from where we started; that is, with the global keyword.
the container around – it stays entirely outside the scope of the objects it creates.
Adding
The process for
Add a new services.php include file to create the container and manage its services.
Define a router service in the container.
Modify the front controller to include the services.php file and use the router service,
Extract creation logic from each page script to the container.
Add a DI Container Include File
we will introduce a new services.php setup file.
Add A Router Service
the front controller creates a Router object, so we will add a router service to the container.
Modify The Front Controller
modify the front controller to load the container and use the router service.
Creado por el container de dependencias
Extract Page Scripts To Services
Create A Container Service
Pick any page script and determine what class it uses to create its $controller instance. Then, in the DI container, create an empty service definition for that class name.
Route The URL Path To The Container Service
Common Questions
How Can We Refine Our Service Definitions?

We can do so by further extracting each part of object creation logic to its own service.
What If There Are Includes In The Page Script?
When we copy the page script logic to the container, we have little choice but to copy them as well.
we can look for commonalities and begin extracting the include logic either to a setup script or to separate classes
we can look for commonalities and begin extracting the include logic either
we can look for commonalities
we can look for commonalities and begin extracting the include logic either to a setup script or to separate classes
we can look for commonalities and begin extracting the include logic either
Can We Reduce The Size Of The services.php File?
make the services.php a series of include calls
Can We Reduce The Size Of The router Service?
we map every URL in the application to a service; if there are hundreds of URLs, there will be hundreds of router lines.
What If We Cannot Update To PHP 5.3?
instead of creating service definitions as closures, we create them as methods on our extended container.
Review and Next Steps
we have completed our modernization process.
We no longer have any page scripts.
application logic has been converted to classes,
only remaining include files are part of the bootstrap and setup process.
All of our object creation logic exists inside a container,
17. Conclusion
    Opportunities for Improvement
    The data source layer is composed of a series of Gateways
    it may be better to restructure these as Data Mappers
    The domain layer is built on top of Transaction Scripts
    We will probably want to begin to tease out the different aspects of our domain logic into a Domain Model
    We may want to convert our view files to a Two Step View
    we may wish to represent the response as a Data Transfer Object that describes our intentions,
    We will want to replace this basic router with a more powerful one.
    Para poder usar urls mas al rstilo rest. Que pasando query params
    We may wish to separate the task of discovering the route information from the task of dispatching that route.
    our dependency injection container is very “manual” in nature.
    We have traded the “low-quality” problems of a spaghetti mess for the “high-quality” problems of an autoloaded, dependency-injected, unit-tested, layer-separated, front-controlled codebase.
    Conversion to Framework

Although switching to a public framework is a little bit like an application rewrite, it should be much easier now that we have a well-separated series of application layers.
in the course of modernizing our legacy application, we have essentially built our own custom-tailored framework.


## Recursos

- [Refactor legacy PHP][1] en Amazon

[1]: https://rchavarria.github.com
