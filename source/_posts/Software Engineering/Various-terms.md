---
title: 'Software Engineering - various terms'
tags:
  - Software Engineering
categories:
  - [Software Engineering, Basics]
date: 2020-07-08
---
# Terms

## function declaration vs definition, parameter type, return type

## Empty variables interpretation

* `null` means nothing - we want no value
* `undefined` declared but not defined - we want default value

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

## Authorization vs Authentication

• **Authentication** describes the process of claiming an identity. That’s what you do when you log in to a service with a username and password, you authenticate yourself.
• **Authorization** on the other hand describes permission rules that specify the access rights of individual users and user groups to certain parts of the system.

## Monkey patching
[https://en.wikipedia.org/wiki/Monkey_patch](https://en.wikipedia.org/wiki/Monkey_patch)
[https://www.audero.it/blog/2016/12/05/monkey-patching-javascript/](https://www.audero.it/blog/2016/12/05/monkey-patching-javascript/)

## Domain-driven design (skrót DDD)
- podejście do tworzenia oprogramowania kładące nacisk na takie definiowanie obiektów i komponentów systemu oraz ich zachowań, aby wiernie odzwierciedlały rzeczywistość. Dopiero po utworzeniu takiego modelu należy rozważyć zagadnienia związane z techniczną realizacją. Podejście to umożliwia modelowanie systemów informatycznych przez ekspertów, którzy znają specyfikę problemu, lecz nie muszą znać się na projektowaniu architektury systemów informatycznych.

## Command–query separation (CQS)
- is a principle of imperative computer programming. It was devised by Bertrand Meyer as part of his pioneering work on the Eiffel programming language. It states that every method should either be a command that performs an action, or a query that returns data to the caller, but not both. In other words, Asking a question should not change the answer.[1] More formally, methods should return a value only if they are referentially transparent and hence possess no side effects.