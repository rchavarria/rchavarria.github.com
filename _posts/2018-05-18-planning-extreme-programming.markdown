---
layout: post
title: "Planning eXtreme Programming"
date: 2018-05-18 05:18
author: Ruben Chavarria
categories:
- Reseñas
---

##### de de Kent Beck y Martin Fowler

[![Planning eXtreme Programming](https://ullizee.files.wordpress.com/2009/11/planning-extreme-programming-xp16590_f.jpg)][1]

### Por qué lo he leído

### De qué trata el libro

### Conclusiones y valoración

### Qué he aprendido

### Frases que me gustaría recordar

## Notas tomadas

Chapter
Chapter 1. Why Plan?
We plan to ensure that we are always doing the most important thing left to do, to coordinate effectively with other people, and to respond quickly to unexpected events.
Why We Should Plan
Planning allows us both to adjust what we do and to coordinate with
Planning allows us both to adjust what we do and to coordinate with others.
What We Need in Planning
In order to carry out the coordination it's vital to have an accurate picture of how far you are along in the plan.
Any software planning technique must try to create visibility,
This means that you need clear milestones,
The Planning Trap
If things don't go according to plan, then the planner is afraid he will be blamed. That fear induces the planner to say that the plan is still on track.
Events happen. Plans change.
Chapter
Unacknowledged Fear Is the Source of All Software Project Failures
If these fears are not put on the table and dealt with, then developers and customer each try to protect themselves by building walls.
Customer Bill of Rights
Programmer Bill of Rights
we must create a culture that makes it possible for programmers and customers to acknowledge their fears and accept their rights and responsibilities.
Chapter 3. Driving Software
Chapter 4. Balancing Power

Our planning process relies on clearly separating the roles of business people and software people. This ensures that business people make all the business decisions and software people make all the technical decisions.
estimating is a technical decision.
Choosing the relative priority between features is a business decision.
Asi que nada de elegir una tecnolohia porque sea cool
Business decisions in planning are Dates Scope Priority
Technical decisions in planning are Estimates If we have the right people making the decisions, planning will go as well as possible. We'll be able to deal with our disasters. We'll do it by reducing the number of disasters as much as possible, by finding out about the disasters as quickly as possible, and by maintaining as many
Technical decisions in planning are Estimates
The Customer
By customer we mean the person who makes the business decisions.
XP planning assumes that the customer is very much part of the team,
Any (XP) project will fail if the customer isn't able to steer.
Finding a Customer
Is willing to accept ultimate responsibility
Is willing to accept ultimate responsibility for the success or failure of the project
Nada d esconderse bajo una pila de requisitos
Guiding the Customer
Trust the developers' estimates,
Never let a date slip.
Provide a little valuable functionality every single release,
Chapter 5. Overviews
Top Down
cycles. Software development is no different. The planning challenge is that there are two cycles that we need to accommodate and synchronizethe business cycle and the development cycle.
The planning challenge is that there are two cycles that we need to accommodate and synchronizethe business cycle and the development cycle.
the business cycle is at least months long.
The development cycle has always been shorter than the business cycle.
Un ciclo de negocio es una release
release.
development cycles an iteration.
Bottom Up
What if we shrunk the whole software development life cycle to microscopic size, say two weeks? We would still have to solve all the problems we had to solve beforespecification, design, implementation, testing, integration, deployment, training, documentationbut now they would be small problems, not big problems, and some of them might disappear entirely.
What if we shrunk the whole software development life cycle to microscopic size, say two weeks?
We will have to do a little of each of them every day.
At the beginning of each iteration the business (remember the balance of power) will pick the most valuable features for the next iteration.
Chapter 6. Too Much to Do
When you are overloaded, don't think of it as not having enough time; think of it as having too much to do. You can't give yourself more time, but you can give yourself less to do,
Chapter 7. Four Variables
In planning software projects, we had to add a variable before we could bring our projects under control: Cost Quality Time Scope We like to think of them as four levers on some big Victorian steam machine. The
We use four variables to help us think about how to control a project: cost, quality, time, and scope. They are interrelated but affect each other in strange ways.
is that the effect of moving a lever is both delayed and nonlinear.
hold everything else the same, and halve the time. So each lever gets its own little instruction manual.
So each lever gets its own little instruction manual.
Lever significa cada una de esas vbles
Cost
is actually several mostly independent levers.
The most powerful lever is people.
more people on the project. This lever, however, suffers from having both a nonlinear effect and a long delay.
suffers from having both a nonlinear effect and a long delay.
nonlinearity comes from the communication overhead
There are other ways to spend money. Spending on tools can be like adding people.
Overtime doesn't help.
for any length of time you will get bitten badly. The big killer is motivation. It's much better to have a motivated programmer work seven hours than a tired, distracted programmer work ten.
The big killer is motivation. It's much better to have a motivated programmer work seven hours than a tired, distracted programmer work ten.
Quality
Quality is really two levers: external and internal quality.
External quality is the quality perceived by the customer.
internal quality. This reflects the quality of the internals of the system: how well it is designed, how good the internal tests are, and so on.
Nothing kills speed more effectively than poor internal quality.
Time and Scope
certainly impossible for exerting any short-term
certainly impossible for exerting any short-term control. Time and scope are left as the best levers to operate.
Time and scope are left as the best levers to operate.
they are placed on very different parts of the machine. The scope lever is right in front of you and just loves to be pushed up.
machine. The scope lever is right in front of you and just loves to be pushed up.
people don't usually realize what's happening until it's too late and the machine is out of control.
La palanca del tiempo esta mmuy escpndida
Planning must make the time lever visible,
You only really know where you are when you are at the end of project. So you need to end the project every few weeksthat's
Shopping for Stories
Chapter 8. Yesterday's Weather
As the basis for your planning, assume you'll
As the basis for your planning, assume you'll do as much this week as you did last week.
Chapter
Chapter 9. Scoping a Project

Making the Big Plan
Break the problem into pieces. Bring the pieces into focus by estimating them. Defer less valuable pieces.
What, Me Worry?
Chapter 10. Release Planning
In release planning the customer chooses a few months' worth of stories, typically focusing on a public release.
Release planning allocates user stories to releases and iterationswhat
Who Does Release Planning?
customer and the programmers.
How Stable Is the Release Plan?
Not at all. The only thing we know for certain about a plan is that development won't go according
Not at all. The only thing we know for certain about a plan is that development won't go according to it.
How Far in Advance Do You Plan?
point going into great detail for years into the future. We prefer to plan one or two
point going into great detail for years into the future. We prefer to plan one or two iterations in advance and one or two releases in advance.
We prefer to plan one or two iterations in advance and one or two releases in advance.
The real decider for how far in advance you should plan is the cost of keeping the plan up-to-date versus the benefit you get when you know that plans are inherently unstable.
How Do You Plan Infrastructure?
evolve the infrastructure as you build the functionality.
De lo contrario pasaras mucho tiempo con la infraestructura y no tendras nada de funcionalidsd
How Do You Store the Release Plan?
set of cards. Each card represents a user story
How Much Can You Put into a Release?
We use the term velocity to represent how much the team can do in an iteration.
Chapter 11. Writing Stories
user story is a chunk of functionality (some people use the word feature) that is of value to the customer.
Principles of Good Stories

Stories must be understandable to the customer.
We like to write user stories on index cards.
The shorter the story the better.
not that you don't need all of those details. You just don't need them all up front.
not that you don't need all of those details. You just don't need them all up front.
It's not that you don't need all of those details. You just don't need them all up front.
Stories need to be of a size that you can build a few of them in each iteration.
The customer must write the story; the developers then estimate the story.
Feedback from Estimation

It is very common for a user to write a story that cannot be easily estimated.
estimate the story. Programmers don't need infinite detail in order to estimate; they just need the customer to translate her needs
Programmers don't need infinite detail in order to estimate; they just need the customer to translate her needs
Programmers don't need infinite detail in order to estimate; they just need the customer to translate her needs into something concrete that they can take action on.
Prioritizing User Stories
wouldn't have written them, now would they? Instead, the customer needs to prepare to answer the question "What would you like us to implement first, and what will we implement later?"
the customer needs to prepare to answer the question "What would you like us to implement first, and what will we implement later?"
Traceability
customer will have to specify acceptance tests
the simpler trace between story and the acceptance tests. If the acceptance tests work, we can safely assume that some code exists that maps to the
the simpler trace between story and the acceptance tests. If the acceptance tests work, we can safely assume that some code exists that maps to the story. If
If the acceptance tests work, we can safely assume that some code exists that maps to the story. If
Splitting User Stories
User Story Adornments
keep our user stories uncluttered.
The Story Writing Process
feeling your way. The process of writing stories is iterative, requiring lots of feedback.
The process of writing stories is iterative, requiring lots of feedback.
Don't be too impressed with your stories. Writing the stories is not the point. Communicating is the point.
Writing the stories is not the point. Communicating is the point.
When Are You Done Writing Stories?
Never,
meaningful choices. Everyone (especially at the beginning of projects) needs to feel heard. If the customer needs to write (quickly write) two years' worth of stories before he feels listened to, so be it.
Everyone (especially at the beginning of projects) needs to feel heard. If the customer needs to write (quickly write) two years' worth of stories before he feels listened to, so be it.
The Disposition of User Stories
Once a user story has been implemented and its acceptance tests are running, the story itself serves no further purpose.
them is probably the best option. Remember that the stories are encoded in far more detail and accuracy in the acceptance tests,
stories are encoded in far more detail and accuracy in the acceptance tests,
Chapter 12. Estimation
Base your story estimates on a similar story you've already done.

The best guide to estimating the future is to look for something that happened in the
The best guide to estimating the future is to look for something that happened in the past that was about the same as the future thing. Then
Estimating the Size of a Story
It doesn't actually matter what units you express the estimate
Estimating How Much You Can Do in an Iteration
The Meaning of Ideal Time
Improving Your Estimates
Chapter 13. Ordering the Stories

The most important stories to do first are the ones that contain the highest business value.
All of these techniques are pretty much useless on an XP project. They are useless because dependencies between tasks do not figure strongly, because of the emphasis on minimal technical commitment and constant growth in the design.
Las tecnicas de las que abla son las clasicas. Que organiza por dependencias y camino critico
Business Value
We want to get a release to the customer as soon as possible. We want this release to be as valuable to the customer as possible.
Determining business value is a decision entirely within the realm of the business people.
a story? The short answer is that we don't; that is, the developers and project managers don't.
the developers and project managers don't.
Technical Risk
As the developers look at the stories they will inevitably start thinking about how they will build them. As they do this they will run the gamut of feelings, all the way from "no problem" to "can't be done." These feelings are important, because they are the manifestation of where the project could go off the rails.
Negotiating Between the Two
Programmers want to tackle high-risk stories first, and customers want to tackle high-value stories first.
programmers' task to make the risk visible, not to make the decision for the customer.
Example Release Plan
Chapter 14. Release Planning Events

Changing the Priorities of Stories
Adding a Story
other methodologies out there, the biggest difference to customers
other methodologies out there, the biggest difference to customers is that they don't have to commit to a detailed specification of everything they want before development begins.
customers is that they don't have to commit to a detailed specification of everything they want before development begins.
Rebuild the Release Plan
but if enough of them mount up that you are sure you aren't going to get everything done, it's time to do something about it.
you aren't going to get everything done, it's time to do something about it.
Chapter 15. The First Plan
The first plan is the hardest
Making the First Plan
and build up the history to make the later plans better. The first plan, however, is always high on expectations and usually low on delivery.
The first plan, however, is always high on expectations and usually low on delivery.
Choosing Your Iteration Length
working, tested codewhich is hard to fudge. But milestones only occur at the end of an iteration. The longer the iteration, the more risk you run of sliding just a little bit out of control.
But milestones only occur at the end of an iteration. The longer the iteration, the more risk you run of sliding just a little bit out of control.
But milestones only occur at the end of an iteration. The longer the iteration, the more risk you run of sliding just a little bit out of control.
Getting Started
Chapter 16. Release Planning Variations
Some local adaptations of the release planning are shorter releases, longer releases, and shorter stories.

encountered. Short Releases Sometimes you can release much more often, maybe every iteration. This can happen for in-house development and also for application service providers where your users are distant but using thin clients and you have close control over the server. Most of this is good news. Each iteration is ready for production, and going into production with each iteration is perfectly feasible. This usually means that you need to have high confidence in your tests and a very automated build process, but if you
Short Releases
each iteration is perfectly feasible. This usually means that you need to have high confidence in your tests and a very automated build process,
you need to have high confidence in your tests and a very automated build process,
With short releases you don't really need any notion of a release at all.
customer spends so much time choosing features for the short term that she misses important long-term needs.
lose strategic vision
However, there is a danger to never having "a release." The customer may lose strategic vision
customer may lose strategic vision
Long Releases
Our first reaction to this reality is to question it. Maybe there is some way to release more frequently.
send intermediate releases to those customers that may be more interested in these versions. Call them service packs or something. That way at least some of your users will use the system in production,
Compartir con norbert
Small Stories
customer finer control over the activities of the team,
Chapter 17. Iteration Planning
Each iteration is planned by breaking down the stories for that iteration into tasks. Tasks are scheduled by asking programmers to sign up for the tasks they want, then asking them to estimate their tasks, then rebalancing as necessary.
The release plan is synchronized to the rhythms of business.
that together tell a good story to the market. The iteration plan is synchronized to the rhythms of programming.
The iteration plan is synchronized to the rhythms of programming.
The release plan is synchronized to the rhythms of business.
Never Slip the Date
principles in planning for Extreme Programming is that the dates are hard dates, but scope will vary.
dates are hard dates, but scope will vary.
Chapter 18. Iteration Planning Meeting
Understanding the Story
facsimile, providing that everyone understands that the narrative is a supplement to conversation not a substitute for it.
narrative is a supplement to conversation not a substitute for it.
tests are the best format for corroborating detail.
Los tests son lo mejor herramienta para ponerse de acuerdo en los dryalles
Listing the Tasks for an Iteration
to break the story down into a few finer-grained tasks. Each task should be a few ideal days of effort. The tasks are development tasks, so they don't need to make sense to the customer.
Each task should be a few ideal days of effort. The tasks are development tasks, so they don't need to make sense to the customer.
You don't need a major design effort here, but you do need just enough to get a good list of tasks.
Antes de programar se puede dar un repaso al codigo que habra que modificar. Hacerlo en grupo
you never plan precisely when each task gets done, or in what order the task gets done.
As long as the tasks are kept short and you can write tests for them, you'll be fine.
Technical Tasks
Measuring the Velocity of a Programmer
Signing Up and Estimating Tasks
The first thing she needs to do is to estimate how long it will take her to do the task.
Be wary of using comparable work from another programmer.
Programmers do not work at the same speed,
Programmers should always assume they have a partner when doing a task,
Programmers should also assume that they aren't done with a task until they have all the unit tests written and passing.
Programmers can sign up for whatever they want to do.
Scut Work
Some project managers on hearing about this "signing up" practice fear there'll be some dirty work that doesn't get done.
Team members may choose to do a more formal rotation to take turns doing unpopular work.
Too Much to Do
Customers can defer a whole story, or they can choose to split a story and defer one of the resulting parts
Too Little to Do
The programmers ask the customer to add some stories.
Chapter 19. Tracking an Iteration

The only thing you know about a plan is that things won't go according to it. So you have to monitor the iteration at regular intervals.
Iteration Progress Check
or (heaven forbid) writing a report. Instead, the tracker should visit each programmer one at a time.
the tracker should visit each programmer one at a time.
Falling Behind
Tracking is passive, until you find that something is up.
look for someone else with time available who is willing to accept the task.
there aren't any great solutions available, you have to go to the customer and tell her the score.
there aren't any great solutions available, you have to go to the customer and tell her the score.
features and tasks that had been scheduled for that time period. After this kick-off day the tasks were written on posters and hung up on the wall, waiting to be ticked off as they were completed. Throughout the iteration programmers asked the customers for clarification of requirements; at the same time, customers nudged the emerging product this way and that as they saw what they had imagined taking shape. When a pair of developers completed a task, they went to the wall poster and crossed it off, and moved on to the next one. Ideal as that might sound, there was a problem. Notice how the developers weren't crossing off tasks when they were done. They were crossing them off when they thought they were done. The collaboration hadn't been taken far enough. In spite of the close cooperation during development, the programmers were taking that final step, that business decision, by themselves. This had unpleasant consequences. After the task had been crossed off, the customers would look at the feature and say, "That doesn't work quite right. It needs a minor adjustment." With the process unclear about how to go back in a situation like this, the customers would simply log the discrepancy as a bug. As time went by, the bug list grew: incompletions, small deficiencies, and simple misunderstandings were being added to the bug list. Management started pressuring the developers to lower the bug count. Developers resented the pressure because many of the items clearly weren't "bugs"; they were just clarifications or even changes of mind. Customers resented having the overhead of the extra tracking. Everybody knew the root of the problem was a communication issue, not a lack of competency. But how to fix it? We were already in constant communication. Finally the project manager, Vraj Mohan, saw the simple solution: It should be the customer, not the developer, who would cross off tasks at completion. This would force the final collaborative step that had been missing from the process. Once this step was instituted, most of the friction that had been developing melted away. Programmers had a much more confident sense of completionif the customer saw the final piece of work and was satisfied, the developers could be sure that they were finished with the task. Customers still wanted changes in features after completion, but now the changes were viewed as enhancements or additional features that they themselves had generated, rather than as bugs that were the fault of the programmers. Sharing the Glory At the end of each iteration, the whole team would gather round and watch the developers demo the work in which each had been involved in the preceding three weeks. This was partly so that everyone could be kept abreast of the latest developments, and partly as a morale boostit's gratifying for the developer-customer team to show off the work they have done together to the rest of the team. We would walk down the task list, and for each crossed-off task, one of the developers from the pair that had worked on the task would step forward and demo the feature. As each task came up to be demoed, there was often a hesitation as the two developers who had paired on the task decided on who would be the one to demo the feature. At one such point, at the end of the third or fourth iteration, there happened to be a long delay. To end the wait, the customer whose feature it was stepped forward and good-naturedly announced that she herself would demo it instead of waiting for the developers to decide. It was done on the spur of the moment and brought a laugh from the team watching on; but as Rob and Kent thought about what had just happened, they realized that this was an excellent idea. Why not always have customers demo their features? It would ensure without a doubt that customers would keep up with the work being done during the iteration. In front of an audience, everyone wants to be prepared for their "performance," so no customers would want to lose track of what progress had been made on their features. This process has become popular. It encourages the customer to keep in closer contact with the developer pair: We have found that customers are more eager to check in with developers to see new work as soon as possible, which tends to lead to closer matching of the customer's vision with the final product. Falling Behind Tracking is passive, until you find that something is up. Up in this case means the programmer realizes she can't complete all the tasks she signed up for. There are plenty of reasons this can happen, but the most important point is to do something about it. The first reaction is to look for someone else with time available who is willing to accept the task. He should then give his own estimate of how much time is needed to finish the task. If his estimate ends up greater than the time available, the problem hasn't been solved yet. If nobody has enough time to take on the task, then the team needs to figure out what to do about it. It's important to let everyone know about the problem, as someone may have a good solution at hand. This is where the stand-up meeting comes in handy. Often a bit of informal juggling of a couple people's time can overcome the problem. If there aren't any great solutions available, you have to go to the customer and tell her the score.
Falling Behind
Tracking is passive, until you find that something is up.
look for someone else with time available who is willing to accept the
look for someone else with time available who is willing to accept the task.
If there aren't any great solutions available, you have to go to the customer and tell her the score.
The key cure to this problem is to get better at estimating, and this can only come with practice and good task records.
When a Programmer Has Extra Time
see if the programmer can help others.
what can be brought forward, either a full story or part of a story.
consider letting him take a break.
When Is the Iteration Done?
When Is a Story Done?
when the function of that story is demonstated to the customer
Chapter 20. Stand-up Meetings

short daily meetings are invaluable for giving everyone an idea of what other people are doing.
Chapter 21. Visible Graphs
Anyone should be able to sense the state of the project by looking at a handful of graphs in the team's working area.
Choosing Which Graphs to Show
When a graph has done its job, drop it.
select the graphs you need and stop producing graphs you don't.
Chapter 22. Dealing with Bugs
Schedule bug fixes with stories so the customer can choose between fixing bugs and adding further functionality.
Dealing with Production Defects
The most important thing is to remove the emotion. A bug report is a request for a change to the deployed system.
Production Support Team
programmers volunteer to focus on fixing bugs. Each programmer spends a couple of iterations in production support,
Each programmer spends a couple of iterations in production support,
Dealing with Critical Bugs
The difficulty is identifying which things really are critical bugs. Only the customer can make this call.
Chapter 23. Changes to the Team

When the team changes, how does that affect your planning?
Coming
Give new team members an iteration or two to get acclimated.
Going
one leaves, reduce
one leaves, reduce your next iteration by 20 percent.
If you have five programmers and one leaves, reduce your next iteration by 20 percent.
If you have five programmers and one leaves, reduce your next iteration by 20 percent.
Splitting the Team
Tamaño Maximo de equipo de 10
Yesterday's Weather will quickly tell you how much cross-team overhead to plan for.
People Growing
XP isn't executed by Plug Compatible Programming Units. It is executed by people, changing people.
what if you put the management tasks on the board alongside the technical tasks
Si todos comparten tareas en el tablon. Unis podran hacer la tareas de otros
Chapter 24. Tools
Stick with simple tools, like pencil, paper, and whiteboard. Communication is more important to success than whizbang.
There are two problems to solve in project management: Keeping track of all data Maintaining communication and relationships between people
Chapter 25. Business Contracts

Traditional business relationships require a little tweaking if you're going to plan and execute a project with
Traditional business relationships require a little tweaking if you're going to plan and execute a project with XP.
Outsourcing
The typical outsourcing contract fixes three of the four variables:[1] [1] Thanks to Dave Cleal for many of the refinements on negotiable scope contracts. Scope Time Cost
quality is the hardest variable to measure, surprises tend to get absorbed by reducing qualitya
the contract could read, "Supplier will have eight programmers work for Customer for two months for $320,000. Scope will be negotiated every two weeks according to the classic book Planning Extreme Programming."
In-House Development
The biggest problem with in-house projects is finding the customer.
If you can't find a single person to act as customer, you will have to have a committee of customers.
Shrink-Wrap
How do you plan when you don't have one customer, you have hundreds, thousands, millions and billions and trillions of customers? XP requires the customer to speak with one voice.
This role is called "product manager"
The key point is that responsibility for resolving conflicts is shifted away from development.
El PM habla con muchos clientes. Negocio. Marketing. Ventas...
Chapter 26. Red Flags
The solutions are all some form of "slow down until you are under control, then speed up again."
Missing Estimates
Are you committing to too much?
they got behind on testing and refactoring
Have you gotten behind on testing and refactoring? If so, you'll see debugging take an increasing percentage of time but an unpredictable percentage.
Customers Won't Make Decisions
out why the customer won't make the decisions. If his priorities are elsewhere, perhaps the whole project doesn't make sense.
Find out why the customer won't make the decisions. If his priorities are elsewhere, perhaps the whole project doesn't make sense.
Defect Reports
you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
requests aplenty, but the software should work as specified. If you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
specified. If you are seeing enough defect reports to disrupt development, slow down until you aren't seeing them.
Not Going End to End
Failing Builds
make the integration environment match the production environment more closely.
Customer Won't Finish
Make three- to four-month release plans that the customer presents to upper management.
Chapter 27. Your Own Process
Once you get comfortable with the basic process, you will grow it to fit your situation more precisely.
Adopt XP planning "by the book." Run for a couple of iterations. Then look at the problems you
Adopt XP planning "by the book." Run for a couple of iterations. Then look at the problems you are having
Adopt XP planning "by the book." Run for a couple of iterations. Then look at the problems you are having and experiment with each iteration.
The beauty of an iterative process with short iterations and lots of data is that you can perform many more experiments,
Take advantage of your data. Play with your process.

## Recursos

- [Planning eXtreme Programming][1] en Amazon

[1]: https://amzn.to/2HKycNs
