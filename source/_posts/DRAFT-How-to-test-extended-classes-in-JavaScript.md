---
title: '[DRAFT] How to test extended classes in JavaScript'
tags:
  - Tests
  - JavaScript
categories:
  - [JavaScript, Tests]
date: 2019-01-01 10:00:00
---

*   [https://blog.arkency.com/2014/09/unit-tests-vs-class-tests/](https://blog.arkency.com/2014/09/unit-tests-vs-class-tests/)
*   [https://martinfowler.com/bliki/UnitTest.html](https://martinfowler.com/bliki/UnitTest.html)
*   testowanie tylko “publicznych” metod klas/obiektów pozwala zaoszczędzić czas na refaktor poprzez brak konieczności zmiany istniejących testów, zapewniając że główna logika API działa dobrze — Existing tests not only helped him to assert correctness of the new solution but more importantly they did not stand in his way during the refactoring. As he admitted, he wouldn’t get it done as quickly as he did had he had to address failing unit tests throughout the process.
*   test “class” units because pragmatically it makes our tests much more stable — like, you don’t need to change test if you extracted something to a method or splitted one coupled class to two. Do you really want to test against structure of your code, or against what the code does? I choose latter solution.
*   About the “Integration Test” and “Unit Test” from Martin Fowler:
“Object-oriented design tends to treat a class as the unit, procedural or functional approaches might consider a single function as a unit. But really it’s a situational thing — the team decides what makes sense to be a unit for the purposes of their understanding of the system and its testing. Although I start with the notion of the unit being a class, I often take a bunch of closely related classes and treat them as a single unit. Rarely I might take a subset of methods in a class as a unit. However you define it doesn’t really matter.” [https://martinfowler.com/bliki/UnitTest.html](https://martinfowler.com/bliki/UnitTest.html)
*   Tests are meant to protect you from regressions and you don’t get that value when you need to update the tests whenever the implementation changes. For the same reason it destroys the point of Red-Green-Refactor approach.
*   Now, would I see value in having a test for the Pricing class directly? Having more tests is good, right? Well, no — tests are code. The more code you have the more you need to maintain. It makes a bigger cost. It also builds a more complex mental model. Low-level tests are often causing more troubles than profit.