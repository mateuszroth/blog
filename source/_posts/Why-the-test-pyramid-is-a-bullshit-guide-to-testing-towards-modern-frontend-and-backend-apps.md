---
title: "Why the test pyramid is a bullshit - guide to testing towards modern frontend and backend\_apps"
tags:
  - Tests
  - Software Engineering
categories:
  - [Softwafe Engineering, Tests]
date: 2019-07-03 14:25:41
---

<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/0*4W87Ed6xZGIuHp4E.png)<figcaption>_source _[_https://martinfowler.com/bliki/TestPyramid.html_](https://martinfowler.com/bliki/TestPyramid.html)</figcaption></figure><!--kg-card-end: image-->> TL;DR; The shape and levels of the test pyramid highly depends on your application (and it mustn’t be a pyramid!) but there are known anti-patterns.

In this guide I want to address the types of testing of web apps especially in the face of the increase of the popularity of Single Page Applications and microservices, the diversified terminology and how we can refer to the well-known test pyramid which will be also covered here. I want to answer question what’s the good approach to test frontend and backend apps that are created by us today but in general and not in relevance to any specific tools.

After reading this article I hope you’ll find why following patterns it’s not always a good solution. I tried to make a precise research about it but if you see anything that can be improved or where I got wrong, please write a comment about it.

### Intro — purpose of testing

We test to verify that a software we develop meets client’s requirements and works as expected. More often to just check if we hadn’t broken something due to our last changes in codebase. Although, when our software is getting more complex, we are not able to test all possible broken cases manually. I’d say, we are able to test it manually but it’s so time-consuming and boring that for sure it will lead to overlook a lot of bugs because of the human factor. That’s why we start to automate and write them. It gives us confidence that we made no mistake in the path of a use case and the automation speeds up the whole process. Both developers and QA engineers write tests. Anyway, we still need to do manual tests because not everything can be covered with automation, so we have also QA manual testers.

### The (not)well-known three

Before we start to talk about the test pyramid let’s introduce the basic three types of tests used within the test pyramid.

#### Unit tests

Unit tests are mostly written by developers and are done in the manner of white-box testing. We have to keep them simple, easy to debug and isolated which means less cases to cover by testing a one method/function at the same time. If we for example test 3 functions at the same time which returns different booleans values then it may give us 2*2*2 = 8 different cases to test. Unit tests gives us fast feedback because units are tested separately in isolated environment with mocked dependencies.

#### But what the heck is a unit?

That is highly dependent on adopted approach to programming. In object-oriented programming (OOP) a unit mostly means a class and main approach is to test public methods of classes. We don’t reason about private methods which are used by the public ones because we treat a class like an indivisible unit. But there are also approaches where people treat single methods as units and that also may be fine in some cases. In the functional programming (FP) we test all functions separately as a function is our smallest unit. We just want to make sure that depending on parameters which we used to call our function it then returns the expected values.

However I think there is no one correct answer. It’s just fine to have agreed on a one term used within your team and stick to it. For me, what we call a unit, it’s just an agreement.

Good advice from [Ham Vocke on the Martin Fowler’s w](https://martinfowler.com/articles/practical-test-pyramid.html)ebsite is to don’t reflect internal code structure within unit tests and tests only for behavior that is observable, so think:

_if I enter values _`_x_`_ and _`_y_`_, will the result be _`_z_`_?_

instead of

_if I enter _`_x_`_ and _`_y_`_, will the method call class A first, then call class B and then return the result of class A plus the result of class B?_

so we can easily refactor and make changes within our codebases.

Often we tend to have test coverage as high as it is needed to fell confident that our codebase is not highly liable to bugs. I here recommend [Kent Beck opinion](https://stackoverflow.com/questions/153234/how-deep-are-your-unit-tests/153565#153565) about how thorough our tests should be.
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/1*NCbDeRM2IwxofXPcu6CejA.png)<figcaption>source [https://auth0.com/blog/testing-react-applications-with-jest/](https://auth0.com/blog/testing-react-applications-with-jest/)</figcaption></figure><!--kg-card-end: image-->

#### Integration tests

That’s a type of tests that makes the most confusion for me. Let’s say we have a React app, what integration tests should cover? What in the case of a monolith serverside app? What in the case of microservices architecture? Is writing some automatic tests on our app’s UI the integration testing? Some definitions say that integration tests are for processes and components but what exactly is a process or a component? They have different meanings regarding an app we’re currently testing and there is no clear answer. We can do integration tests of our whole environment (client, server side, database, etc.) but it tends to be called the end to end testing. For me testing few main parts of whole system together like database and server was integration testing and that’s how I’ve been thinking of them a long time from what I’ve learned on university studies and what you’ll find mostly on the Internet. However, in the microservices world we often tend to write tests of integration between our several serverside-services apps. Hence, some people call integration tests as **components or services tests**. I feel there is no one right term since there are lot of variations and they are mostly related to the architecture of a system. One approach is to test a lot of parts of our system at once and another just to test two parts of a system at once. One part can be from external service but it’s used by our system and needs it to work properly so it’s an inseparable part of our system and needs to be tested just the same as the parts that we created ourselves. We can still treat integration tests as white box tests since we test components of our box like server and database which are the part of our whole box — so we know something about the structure of our box. Still, some people call them black box and that’s still may be fine as we treat for example backend and database as something we don’t know implementation details. Let’s postpone more concerns about them until we I think through the test pyramid.

#### End to end tests (E2E)

Called also sometimes UI tests but not always meaning the same. In the case of web apps end to end tests are performed on working instance of our application what involves also the serverside part. They are usually executed in a browser and they perform operations that simulates popular user paths within our app.

Opposite to unit and integration tests they don’t give us exact feedback. They just inform us overall what parts of UI fail no referring back to the frontend or the backend code. Each failing part needs to be manually checked first for errors before reporting a bug. That tests are hard to debug and slow, so we often don’t cover the whole app with them. They are a lot more expensive because writing an automation takes 10 to 50 times more than writing a scenario of a manual test.

But basically what differs them from integration tests? We still test integration between parts of our system — modules of our code, UI with frontend logic, frontend integration with backend. Is it different category or just more general type of integration tests? I’ll leave you with those doubts ;)

### The test pyramid

The test pyramid was first mentioned in Mike Cohn’s book _Succeeding with Agile_. He recommends that applications should be covered by a lot of unit tests which is the base of our tests. Then we write integration (service) tests and the peak is made from E2E (UI) tests. These are all of the type functional and automated tests.
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/0*4W87Ed6xZGIuHp4E.png)<figcaption>_source _[_https://martinfowler.com/bliki/TestPyramid.html_](https://martinfowler.com/bliki/TestPyramid.html)</figcaption></figure><!--kg-card-end: image-->

I like also to look at the test pyramid upside down **as a bug filter** where bugs not detected on a one stage are going to be detected on the next stage.
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/1*kwXazFfzwPHWpJ0oZ8gHDw.png)<figcaption>the testing pyramid as a filter, source [https://twitter.com/noahsussman/status/836612175707930625](https://twitter.com/noahsussman/status/836612175707930625)</figcaption></figure><!--kg-card-end: image-->

The test pyramid was the answer for the issue of having a lot of E2E/UI tests that were for example recorded by a special software. They are causing a definite increase time of building, are really brittle — prone to every change in the UI and gives deficient feedback about encountered errors. So you should write much more unit tests which are faster and then you catch other on a thin layer of E2E tests which cover as much main features as they can. The anti-pattern where our codebase is barely covered with unit tests make a shape of an ice cream cone which is overflowing with manual and automated GUI tests. Unfortunately, it’s a common situation in many projects. Effects are tragic, after few years of no writing tests adding 50 lines of code make them as much time-consuming as adding 5000 or 50000 lines in the past what is painful for developers and not understood by business. Release process takes longer due to slow GUI testing and still lets slip bugs that causes lot of frustration for end users who finally will abandon your product. Finally, inevitably the development of the app will be suspended and all sources addressed for bug fixing and refactoring. It’s your responsibility to write as much unit tests early on in the project. Although in cases of pressure from upper management, it’s your duty to fight for paying off technical debt as early as you can negotiate to prevent such situations.
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/1*k1na189FYze-QKwpWekQVw.png)<figcaption>the ice-cream cone anti-pattern, source: [https://james-willett.com/2016/09/the-evolution-of-the-testing-pyramid/](https://james-willett.com/2016/09/the-evolution-of-the-testing-pyramid/)</figcaption></figure><!--kg-card-end: image-->

As you can see in the diagram of the ice cream cone anti-pattern, there is also the addition of manual tests to the original test pyramid. Currently, it’s often pattern to extend the original test pyramid which is fully automated by adding some manual tests. I believe manual tests are necessary to test newly introduced bugs and some cases that can’t be covered by automated tests.
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/1*6HTj6mBJAcME722MW-tb1g.png)<figcaption>source: [https://james-willett.com/2016/09/the-evolution-of-the-testing-pyramid/](https://james-willett.com/2016/09/the-evolution-of-the-testing-pyramid/)</figcaption></figure><!--kg-card-end: image-->

As the service tests layer is split often into 3 layers in object-oriented serverside apps: API, Integration and Component, how can we treat modern frontend apps and is there any right pyramid for that?

#### **Frontend testing**
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/1*TuU-H8ZK2YQf80WOksLqwQ.png)<figcaption>two-level test pyramid may be a solution for frontend&nbsp;apps</figcaption></figure><!--kg-card-end: image-->

The pyramid where we have only two layers: unit and E2E tests with isolated integration tests seems pretty straightforward and still may be accurate to some types of apps which have no services to integrate. It may happen that there are needed some integration tests but there will be less of them than E2E tests. In this approach, while testing a frontend app, we treat logic, stores and UI components always as separated units. However, there is also another “pyramid” worth mentioning, that was presented by Kent C. Dodds is **the testing trophy**:
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/0*ucVRlPUm_9nM6F29)<figcaption>The Testing Trophy for frontend apps, source: [https://twitter.com/kentcdodds/status/960723172591992832/photo/1](https://twitter.com/kentcdodds/status/960723172591992832/photo/1)</figcaption></figure><!--kg-card-end: image-->

By static tests he means code linters and formatters and also type checkers (in JavaScript he mentioned flow but you can use TypeScript instead). They catch typos and type errors as you write and modify code. In this approach he proposes to write more integration tests between components and logic because these two are often brittle. A button in a component works but action it’s handling and mutating some data may not. He says integration tests strike a great balance on the trade-offs between confidence, speed and expense. Is it good approach? Does it look for you like the universal solution for frontend apps nowadays? I believe this style of testing may work for some apps, but for others not. Without understanding your codebase, common issues and then deciding about the approach to testing, following these patterns may make you go wrong way.

**Microservices testing**
> More modern software development organisations have found ways of scaling their development efforts by spreading the development of a system across different teams. Individual teams build individual, loosely coupled services without stepping on each others toes and integrate these services into a big, cohesive system. The more recent buzz around microservices focuses on exactly that.
> The Practical Test Pyramid, Ham Vocke, [https://martinfowler.com/articles/practical-test-pyramid.html](https://martinfowler.com/articles/practical-test-pyramid.html)

Another pyramid which I encountered during my research was related to microservices architecture. André Schaffer in [his article on Spotify Labs blog](https://labs.spotify.com/2018/01/11/testing-of-microservices/) presented the microservices testing honeycomb:
<!--kg-card-begin: image--><figure class="kg-card kg-image-card kg-card-hascaption">![](https://cdn-images-1.medium.com/max/1600/0*bHkfFls3yRSgrRVT)<figcaption>The Microservices Testing Honeycomb, source [https://labs.spotify.com/2018/01/11/testing-of-microservices/](https://labs.spotify.com/2018/01/11/testing-of-microservices/)</figcaption></figure><!--kg-card-end: image-->

In this approach we focus on integration tests. We want to be sure that our services work together well and the implementation details of them are not so important. They should be easy to change and refactor without causing bugs in another services. He mentions that trade-off is a decrease in execution of tests however he believes the time is paid off by a faster coding and ease of maintenance. I’d say that in this approach we treat services as units. The type of tests where we test APIs between services we call **contract tests**.

### Summary

As we went through several types of tests pyramid, I almost sure you’ve noticed the correlation between tests and the app we want to test. And basically it’s the essence: we shouldn’t follow any patterns before thinking and understanding what we want to test. However, writing tests is crucial. As fast as you understand it, your life will be more pleasant in case of development of your growing app.
<!--kg-card-begin: hr-->

* * *
<!--kg-card-end: hr-->

Sources:

*   Mike Cohn, Succeeding with Agile: Software Development Using Scrum, Addison-Wesley Professional, 2009
*   Testing of Microservices, André Schaffer, [https://labs.spotify.com/2018/01/11/testing-of-microservices/](https://labs.spotify.com/2018/01/11/testing-of-microservices/)
*   What is functional testing with example?, Neha Sharma, [https://www.quora.com/What-is-functional-testing-with-example/answer/Neha-Sharma-3421](https://www.quora.com/What-is-functional-testing-with-example/answer/Neha-Sharma-3421)
*   3 typy testów, które musisz zrozumieć, by robić efektywne TDD, Wojciech Zawistowski, [https://it.esky.pl/programowanie/3-typy-testow-ktore-musisz-zrozumiec-by-robic-efektywne-tdd/](https://it.esky.pl/programowanie/3-typy-testow-ktore-musisz-zrozumiec-by-robic-efektywne-tdd/)
*   White-box testing, Wikipedia, [https://en.wikipedia.org/wiki/White-box_testing](https://en.wikipedia.org/wiki/White-box_testing)
*   Black Box Testing, Software testing fundamentals, [http://softwaretestingfundamentals.com/black-box-testing/](http://softwaretestingfundamentals.com/black-box-testing/)
*   How deep are your unit tests?, Kent Beck, [https://stackoverflow.com/questions/153234/how-deep-are-your-unit-tests/153565#153565](https://stackoverflow.com/questions/153234/how-deep-are-your-unit-tests/153565#153565)
*   Błędy popełniane przy automatyzacji testów, Radek Smilgin, [http://testerzy.pl/baza-wiedzy/bledy-popelniane-przy-automatyzacji-testow](http://testerzy.pl/baza-wiedzy/bledy-popelniane-przy-automatyzacji-testow)
*   TestPyramid, Martin Fowler, [https://martinfowler.com/bliki/TestPyramid.html](https://martinfowler.com/bliki/TestPyramid.html)
*   Test Pyramid as a Risk Filter, Amit Kulkarni, [https://amtoya.com/blogs/test-pyramid-as-a-risk-filter/](https://amtoya.com/blogs/test-pyramid-as-a-risk-filter/)
*   Piramida automatyzacji testów, Code Coverage, [http://pisz-kod.pl/2018/06/07/piramida-automatyzacji-testow-code-coverage/](http://pisz-kod.pl/2018/06/07/piramida-automatyzacji-testow-code-coverage/)
*   The testing pyramid, Automation Panda, [https://automationpanda.com/2018/08/01/the-testing-pyramid/](https://automationpanda.com/2018/08/01/the-testing-pyramid/)
*   The Evolution of the Testing Pyramid, James Willett, [https://james-willett.com/2016/09/the-evolution-of-the-testing-pyramid/](https://james-willett.com/2016/09/the-evolution-of-the-testing-pyramid/)
*   Functional Testing Vs Non-Functional Testing: What’s the Difference?, [https://www.guru99.com/functional-testing-vs-non-functional-testing.html](https://www.guru99.com/functional-testing-vs-non-functional-testing.html)
*   What is functional testing with example?, [https://www.quora.com/What-is-functional-testing-with-example](https://www.quora.com/What-is-functional-testing-with-example)
*   Acceptance Testing, Software testing fundamentals, [http://softwaretestingfundamentals.com/acceptance-testing/](http://softwaretestingfundamentals.com/acceptance-testing/)
*   Sanity Testing Vs Smoke Testing: Introduction &amp; Differences, [https://www.guru99.com/smoke-sanity-testing.html](https://www.guru99.com/smoke-sanity-testing.html)
*   Functional Testing, [https://www.techopedia.com/definition/19509/functional-testing](https://www.techopedia.com/definition/19509/functional-testing)
*   Snapshot testing, [https://jestjs.io/docs/en/snapshot-testing](https://jestjs.io/docs/en/snapshot-testing)
*   Write tests. Not too many. Mostly integration., Kent C. Dodds, [https://blog.kentcdodds.com/write-tests-not-too-many-mostly-integration-5e8c7fff591c](https://blog.kentcdodds.com/write-tests-not-too-many-mostly-integration-5e8c7fff591c)
*   Performance Testing Tutorial: What is, Types, Metrics &amp; Example, [https://www.guru99.com/performance-testing.html](https://www.guru99.com/performance-testing.html)
*   Load Testing Tutorial: What is? How to? (with Examples), [https://www.guru99.com/load-testing-tutorial.html](https://www.guru99.com/load-testing-tutorial.html)
*   Manual Testing Tutorial for Beginners: Concepts, Types, Tool, [https://www.guru99.com/manual-testing.html](https://www.guru99.com/manual-testing.html)