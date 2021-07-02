---
title: 'Software Engineering notes'
tags:
  - Software Engineering
categories:
  - [Software Engineering, Basics]
date: 2020-07-18 10:00:00
---

# Truths
- Product teams focusing on velocity may argue that in the future they will reach a place where they have time to circle back to fix technical debt. This is never true, there is always pressure. A team needs to consciously decide to make stability a part of value delivery, otherwise lack of stability will become part of the team’s culture.
- A mistake early on in the project regarding the architecture may cost a lot in terms of time spent refactoring the codebase later.

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

# Design Patterns

[List of design patterns](https://en.wikipedia.org/wiki/Software_design_pattern#Classification_and_list)
[Source #1 - Common Design Patterns for Android with Kotlin](https://www.raywenderlich.com/470-common-design-patterns-for-android-with-kotlin)

## Creational patterns
They define how you create objects.

* **Builder**
* **Dependency Injection** - explained below
* **Singleton**

## Structural patterns
They define how you compose objects.

* **Adapter** - this pattern lets two incompatible classes work together by converting the interface of a class into another interface the client expect
* **Facade** - The Facade pattern provides a higher-level interface that makes a set of other interfaces easier to use -> for example a repository in Android project can be a facade
* **DAO** - a design pattern for writing objects that access data
  * You should use DAOs. The pattern lends itself to **modularized** code. You keep all your persistence logic in one place (separation of concerns, fight leaky abstractions). You allow yourself to test data access separately from the rest of the application. And you allow yourself to test the rest of the application isolated from data access (i.e. you can mock your DAOs).

## Behavioral patterns
They define how you coordinate object interactions.

* **Command** - Similarly, the Command pattern lets you issue requests without knowing the receiver. You encapsulate a request as an object and send it off; deciding how to complete the request is an entirely separate mechanism.
  * <img src="https://koenig-media.raywenderlich.com/uploads/2015/07/EventBus-Publish-Subscribe.png" width="500px">
  * [How to create event bus](https://www.raywenderlich.com/470-common-design-patterns-for-android-with-kotlin#toc-anchor-010)
* **Observer** - The Observer pattern defines a one-to-many dependency between objects. When one object changes state, all of its dependents are notified and updated automatically.
* **Model View Controller**
* **Model View ViewModel** - The ViewModel object is the “glue” between the model and view layers, but **operates differently than the Controller component. Instead, it exposes commands for the view and binds the view to the model. When the model updates, the corresponding views update as well via the data binding**. Similarly, as the user interacts with the view, the bindings work in the opposite direction to automatically update the model. This reactive pattern removes a lot of glue code.

### Dependency Injection & Dependency Inversion principle explained
```kotlin
class Parent {
    private val child = Child()
}
```
A `Parent` instance creates its child field when it’s instantiated. The `Parent` instance is dependent on the concrete implementation of `Child` and on configuring the child field to use it.

**This presents a coupling or dependency of the `Parent` class on the `Child` class**. If the setup of a `Child` object is complex, all that complexity will be reflected within the `Parent` class as well. You will need to edit `Parent` to configure a `Child` object.

If the `Child` class itself depends on a class `C`, which in turn depends on class `D`, then all that complexity will propagate throughout the code base and hence result in a tight coupling between the components of the application.

**Dependency Injection is the term used to describe the technique of loosening the coupling** just described. In the simple example above, only one tiny change is needed:
```kotlin
class Parent(private val child: Child)
```

Voilà — that’s dependency injection at its core!

There is also **Dependency Inversion principle**. The gist of the Dependency Inversion principle is that **it is important to depend on abstractions rather than concrete implementations**. In the simple example above, this means changing `Child` to a Kotlin interface rather than a `Kotlin` class. With this change, many different types of concrete `Child` type objects that adhere to the `Child` interface can be passed into the `Parent` constructor.

[Source - Dependency Injection in Android with Dagger 2 and Kotlin](https://www.raywenderlich.com/262-dependency-injection-in-android-with-dagger-2-and-kotlin#toc-anchor-003)

# Empty variables interpretation

* `null` means nothing - we want no value
* `undefined` declared but not defined - we want default value

# Qualities of well written code

Write a code like someone after you who you don't know would read the code.

Well written code is easy to maintain, easy to test, very cohesive, decoupled and redable.

* readability / understandability (czytelność, zrozumiałość) vs obscurity (zaciemnienie)
* clean, readable and concise code - czysty, czytelny, zwięzły kod
* complexity (złożoność)
* maintainability (utrzymywalność)
* reliability / testability (niezawodność, testowalność)
* reusability - decoupled and reusable code is preferred
* coupling and code interdependence
* performance
* [https://en.wikipedia.org/wiki/No_Silver_Bullet](https://en.wikipedia.org/wiki/No_Silver_Bullet) essential vs accident complexity
* robustness - the ability of a computer system to cope with errors during execution and cope with erroneous input
* concise vs explicit
* **abstractions are bad**

PEP20 — The Zen of Python
[https://www.python.org/dev/peps/pep-0020](https://www.python.org/dev/peps/pep-0020/)/

# System infrastructure

* scalability - skalowalność
* performance - wydajność
* stability - stabilność
* reliability - niezawodność
* flexibility - jak łatwo się zmienia np. w przypadku mikroserwisów ilość jednostek jednego komponentu/serwisu, czy np. zmiana usługodawcy

# Terms

* function declaration vs definition, parameter type, return type

## coupling (miara współzależności)

In software engineering, **coupling** is **the degree of interdependence between software modules**; a **measure of how closely connected two routines or modules are**; _the strength of the relationships_ between modules.

Coupling is usually **contrasted with cohesion**. **Low coupling often correlates with high cohesion**, and vice versa. Low coupling is often a sign of a **well-structured computer system and a good design**, and when combined with high cohesion, supports the general goals of high readability and maintainability.

## cohesion (miara spójności)

In computer programming, cohesion refers to **the degree to which the elements inside a module belong together**. In one sense, it is a measure of the strength of relationship between the methods and data of a class and some unifying purpose or concept served by that class. In another sense, it is a measure of the strength of relationship between the class's methods and data themselves.

Cohesion is an ordinal type of measurement and is usually described as “high cohesion” or “low cohesion”. Modules with high cohesion tend to be preferable, because **high cohesion is associated with several desirable traits of software including robustness, reliability, reusability, and understandability**. In contrast, low cohesion is associated with undesirable traits such as being difficult to maintain, test, reuse, or even understand.

## loose coupling

In computing and systems design a loosely coupled system is one in which each of its components has, or makes use of, **little or no knowledge of the definitions of other separate components**. Subareas include the coupling of classes, interfaces, data, and services. Loose coupling is the opposite of tight coupling.

## big ball of mud

A **big ball of mud** is a software system that **lacks a perceivable architecture**. Although undesirable from a software engineering point of view, such systems are common in practice due to **business pressures, developer turnover and code entropy**. They are a type of design anti-pattern.

## software entropy

The second law of thermodynamics, in principle, states that a closed system's disorder cannot be reduced, **it can only remain unchanged or increase**. A measure of this disorder is entropy. This law also seems plausible for software systems; **as a system is modified, its disorder, or entropy, tends to increase. This is known as software entropy**.

The process of code refactoring can result in stepwise reductions in software entropy.

**Software rot,** also known as code rot, software erosion, software decay or software entropy is either a slow deterioration of software performance over time or its diminishing responsiveness that will eventually lead to software becoming faulty, unusable, or in need of upgrade.

## feature creep

**Feature creep is the excessive ongoing expansion or addition of new features in a product,**[1] especially in computer software, videogames and consumer and business electronics. These extra features go beyond the basic function of the product and can result in software bloat and over-complication, rather than simple design.

## software brittleness

In computer programming and software engineering, software brittleness is the increased difficulty in fixing older software that may appear reliable, **but fails badly when presented with unusual data or altered in a seemingly minor way**. 

## first-class functions

In computer science, a programming language is said to have first-class functions if it **treats functions as first-class citizens**. This means the language supports **passing functions as arguments to other functions, returning them as the values from other functions, and assigning them to variables or storing them in data structures**.[1] Some programming language theorists require support for anonymous functions (function literals) as well.[2] In languages with first-class functions, the names of functions do not have any special status; they are treated like ordinary variables with a function type.[3]
First-class functions are a necessity for the [functional programming](https://en.m.wikipedia.org/wiki/Functional_programming) style, in which the use of [higher-order functions](https://en.m.wikipedia.org/wiki/Higher-order_function) is a standard practice. A simple example of a higher-ordered function is the [map](https://en.m.wikipedia.org/wiki/Map_(higher-order_function)) function, which takes, as its arguments, a function and a list, and returns the list formed by applying the function to each member of the list. For a language to support _map_, it must support passing a function as an argument.
Source [https://en.m.wikipedia.org/wiki/First-class_function](https://en.m.wikipedia.org/wiki/First-class_function)

## higher order function

a function taking another function as argument is called a higher-order function

# Authorization vs Authentication

• **Authentication** describes the process of claiming an identity. That’s what you do when you log in to a service with a username and password, you authenticate yourself.
• **Authorization** on the other hand describes permission rules that specify the access rights of individual users and user groups to certain parts of the system.

# Software problems

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
* pros if language offers **developing**, **refactoring** and **debugging** is fast and easy
* pros if language offers **strict type system** and **compile-time error checks**, C# is more potent than JavaScript

# Uncommon terms

* **Monkey patching**
[https://en.wikipedia.org/wiki/Monkey_patch](https://en.wikipedia.org/wiki/Monkey_patch)
[https://www.audero.it/blog/2016/12/05/monkey-patching-javascript/](https://www.audero.it/blog/2016/12/05/monkey-patching-javascript/)
* **Domain-driven design (skrót DDD)** – podejście do tworzenia oprogramowania kładące nacisk na takie definiowanie obiektów i komponentów systemu oraz ich zachowań, aby wiernie odzwierciedlały rzeczywistość. Dopiero po utworzeniu takiego modelu należy rozważyć zagadnienia związane z techniczną realizacją. Podejście to umożliwia modelowanie systemów informatycznych przez ekspertów, którzy znają specyfikę problemu, lecz nie muszą znać się na projektowaniu architektury systemów informatycznych.
* **Command–query separation (CQS)** is a principle of imperative computer programming. It was devised by Bertrand Meyer as part of his pioneering work on the Eiffel programming language. It states that every method should either be a command that performs an action, or a query that returns data to the caller, but not both. In other words, Asking a question should not change the answer.[1] More formally, methods should return a value only if they are referentially transparent and hence possess no side effects.