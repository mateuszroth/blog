---
title: 'Microservices'
tags:
  - Backend
  - Microservices
categories:
  - [Backend]
date: 2021-07-05
---
# Microservices
* a software design architecture that breaks apart monolithic systems
* applications are built as collections of loosely coupled services
* data moves between microservices using “dumb pipes” such as an event broker and/or a lightweight protocol like REST

## Advantages
* teams can develop, maintain, and deploy each microservice independently
* scalability, you can scale them separately; the cost of scaling is comparatively less than the monolithic architecture
* faster development cycles - easier deployment and debugging
* speed up your CI/CD pipeline against big monolithic apps
* it’s easier to maintain and debug a lightweight microservice than a complex application
* isolated services have a better failure tolerance

## Disadvantages
* communication between microservices can mean poorer performance, as sending messages back and forth comes with a certain overhead
* microservice has all the associated complexities of the distributed system
* complex testing over a distributed environment; while unit testing may be easier with microservices, integration testing is not
* up-front costs may be higher with microservices

## Sources
* https://raygun.com/blog/what-are-microservices/
* https://solace.com/blog/microservices-advantages-and-disadvantages/
* https://cloudacademy.com/blog/microservices-architecture-challenge-advantage-drawback/