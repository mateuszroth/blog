---
title: 'Software Engineering - architecture and software design'
tags:
  - Software Engineering
categories:
  - [Software Engineering, Basics]
date: 2021-07-08
---
# Truths
- Product teams focusing on velocity may argue that in the future they will reach a place where they have time to circle back to fix technical debt. This is never true, there is always pressure. A team needs to consciously decide to make stability a part of value delivery, otherwise lack of stability will become part of the team’s culture. [source](https://productcoalition.com/agile-gone-wrong-725c3f0dd8c0?gi=3fe19950694e)
- A mistake early on in the project regarding the architecture may cost a lot in terms of time spent refactoring the codebase later. [source](https://selleo.com/blog/why-choose-nest-js-as-your-backend-framework)

# Qualities of well written code

Write a code like someone after you who you don't know would read the code.

Well written code is easy to maintain, easy to test, very cohesive, decoupled and redable.

* readability / understandability (pl. *czytelność, zrozumiałość*) vs obscurity (pl. *zaciemnienie*)
* clean, readable and concise code - pl. *czysty, czytelny, zwięzły kod*
* complexity (pl. *złożoność*)
* maintainability (pl. *utrzymywalność*)
* reliability / testability (pl. *niezawodność, testowalność*)
* reusability - decoupled and reusable code is preferred
* coupling and code interdependence
* performance
* [https://en.wikipedia.org/wiki/No_Silver_Bullet](https://en.wikipedia.org/wiki/No_Silver_Bullet) essential vs accident complexity
* robustness - the ability of a computer system to cope with errors during execution and cope with erroneous input
* concise vs explicit
* too much **abstractions are bad**

PEP20 — The Zen of Python
[https://www.python.org/dev/peps/pep-0020](https://www.python.org/dev/peps/pep-0020/)/

# System infrastructure qualities

* scalability - pl. *skalowalność*
* performance - pl. *wydajność*
* stability - pl. *stabilność*
* reliability - pl. *niezawodność*
* flexibility - pl. *jak łatwo się zmienia np. w przypadku mikroserwisów ilość jednostek jednego komponentu/serwisu, czy np. zmiana usługodawcy*

# Common software development problems

* business pressures
* developer turnover
* code entropy
* developers productivity
* errors tracking and detecting
* infrastructure cost and predicting spikes
* development cost
* enterprise level app - is computer software used to satisfy the needs of an organization rather than individual users

# Languages features

* pros if language offers excellent **code analysis support** and **comprehensive editors/IDEs**
* pros if **developing**, **refactoring** and **debugging** is fast and easy
* pros if language offers **strict type system** and **compile-time error checks**, C# is more potent than JavaScript

# Codebase architecture approaches
* [Hexagonal Architecture](https://alistair.cockburn.us/hexagonal-architecture/)
* [The Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html):
  * (Recommended architecture approaches) They all have the same objective, which is the **separation of concerns**. They all achieve this **separation by dividing the software into layers**. Each has at least one layer for business rules, and another for interfaces.
  * Independent of Frameworks
  * Testable
  * Independent of UI
  * Independent of Database
  * Independent of any external agency
  * Overall: The Dependency Rule always applies. Source code dependencies always point inwards. As you move inwards the level of abstraction increases. The outermost circle is low level concrete detail. As you move inwards the software grows more abstract, and encapsulates higher level policies. The inner most circle is the most general.

# GoF Rules
* "**Program to an 'interface'**, not an 'implementation'." (Gang of Four 1995:18)
  * clients remain unaware of the specific types of objects they use, as long as the object adheres to the interface
  * clients remain unaware of the classes that implement these objects; **clients only know about the abstract class(es) defining the interface**
  * Use of an interface also leads to dynamic binding and polymorphism, which are central features of object-oriented programming.
* **Composition over inheritance**: "Favor 'object composition' over 'class inheritance'." (Gang of Four 1995:20)
  * The authors refer to inheritance as white-box reuse, with white-box referring to visibility, because the internals of parent classes are often visible to subclasses. In contrast, the authors refer to object composition (in which objects with well-defined interfaces are used dynamically at runtime by objects obtaining references to other objects) as black-box reuse because no internal details of composed objects need be visible in the code using them.
  * The authors discuss the **tension between inheritance and encapsulation** at length and state that in their experience, **designers overuse inheritance** (Gang of Four 1995:20).
  * "Because **inheritance exposes a subclass to details of its parent's implementation, it's often said that 'inheritance breaks encapsulation'**". (Gang of Four 1995:19).
  * They **warn that the implementation of a subclass can become so bound up with the implementation of its parent class that any change in the parent's implementation will force the subclass to change**.
  * Furthermore, they claim that a way to avoid this is to inherit only from abstract classes—but then, they point out that there is minimal code reuse.
  * Using inheritance is recommended mainly when adding to the functionality of existing components, reusing most of the old code and adding relatively small amounts of new code.
*  "Dynamic, highly parameterized software is harder to understand and build than more static software." (Gang of Four 1995:21)
* The authors further distinguish between 'Aggregation', where one object 'has' or 'is part of' another object (implying that an aggregate object and its owner have identical lifetimes) and acquaintance, where one object merely 'knows of' another object. 
  * Acquaintance is a weaker relationship than aggregation and suggests much looser coupling between objects, which can often be desirable for maximum maintainability in a design.
* A primary criticism of Design Patterns is that its patterns are simply workarounds for missing features in C++, replacing elegant abstract features with lengthy concrete patterns, essentially becoming a "human compiler" or "generating by hand the expansions of some macro".
