---
title: 'Design Patterns'
tags:
  - Software Engineering
  - Design Patterns
categories:
  - [Software Engineering, Basics]
date: 2020-07-08
---
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
