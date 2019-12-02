---
title: Node.js basics
tags:
  - Backend
  - Node.js
categories:
  - [Node.js, Basics]
date: 2019-10-24 22:33:05
---

# What is Node.js and its pros and cons

Most of the information below is taken from [Netguru blog](https://www.netguru.com/blog).

## What is

Node.js’ famous **asynchronous I/O **and its **single-threaded event loop** models that can efficiently **handle concurrent requests**. Node.js is based on an **event-driven**, **non-blocking I/O model**, and **uses only a single CPU core**. The non-blocking IO system lets you process numerous requests concurrently.
> That’s how we can conclude Node.js is single-threaded but **in the background it uses _<em>multiple threads_</em> to execute asynchronous code with the help of the libuv library. **Only the event loop is single-threaded.
> [https://medium.com/better-programming/is-node-js-really-single-threaded-7ea59bcc8d64](https://medium.com/better-programming/is-node-js-really-single-threaded-7ea59bcc8d64)> While Node.js itself is multithreaded -- I/O and other such operations run from a thread pool -- JavaScript code executed by Node.js runs, for all practical purposes, in a single thread. This isn't a limitation of Node.js itself, but of the V8 JavaScript engine and of JavaScript implementations generally.
> [https://stackoverflow.com/a/40029919](https://stackoverflow.com/a/40029919)> The single threaded, async nature does make things complicated. But do you honestly think it's more complicated than threading? One race condition can ruin your entire month! Or empty out your thread pool due to some setting somewhere and watch your response time slow to a crawl! Not to mention deadlocks, priority inversions, and all the other gyrations that go with multithreading.
> [https://stackoverflow.com/a/17959746](https://stackoverflow.com/a/17959746)> The main functionality differentiation between NodeJs based servers and other IIS/ Apache based servers, **NodeJs for every connection request do not create a new thread** instead it receives all request on single thread and delegates it to be handled by many background workers to do the task as required.
> [https://codeburst.io/how-node-js-single-thread-mechanism-work-understanding-event-loop-in-nodejs-230f7440b0ea](https://codeburst.io/how-node-js-single-thread-mechanism-work-understanding-event-loop-in-nodejs-230f7440b0ea)

Node.js comes with many **APIs suitable for backend development**, e.g. the support for **file systems, http requests, streams, child processes**, etc. Browsers do offer some basic support for file systems or http requests, but those are usually limited due to security concerns.

More:

*   Node.js event loop phases explained [https://codeburst.io/how-node-js-single-thread-mechanism-work-understanding-event-loop-in-nodejs-230f7440b0ea](https://codeburst.io/how-node-js-single-thread-mechanism-work-understanding-event-loop-in-nodejs-230f7440b0ea)

## Pros

Nowadays it is possible to write both front-end and back-end of web applications in Javascript, making app deployment much easier and more efficient. 

Node.js as your server technology gives your team a great boost that comes from **using the same language on both the front end and the back end**. This, means that** your team is more efficient and cross-functional**, which, in turn, leads to **lower development costs**.

Node’s ability to **process many requests with low response times,** as well as **sharing things such as validation code between the client and server**, make it a great fit for modern web applications that carry out lots of processing on the client’s side.

For SPAs apps Node.js would only return the index page (index.html) while data would be sent via REST interfaces and controllers implemented server-side. From the design point of view, such approach will ensure the **clear separation of concerns (SoC) between models, controllers, and views** with all data-related services implemented server-side.

Node.js is especially **popular in real-time applications** or when we seek a **fast and scalable solution**. Node.js. An event-driven, non-blocking server was a good solution for an **instant propagation of updates**, which required **holding a lot of open connections**.

In particular, Node **has a powerful Event API **that facilitates creating certain kinds of objects (“emitters”) that periodically emit named events “listened” by event handlers. Thanks to this functionality, Node.js makes it **easy to implement server-side events and push notifications** widely used in instant messaging and other real-time applications.

Node’s event-based architecture also **works well with the WebSockets protocol **that facilitates a fast two-way exchange of messages between the client and the server via one open connection. By installing WebSockets libraries on the server and the client side, you can implement real-time messaging that has lower overheads and latency, and faster data transfer than most other, more conventional, solutions.

IoT developers working in data-intensive scenarios can leverage the **low resource requirements of Node.js**. **Low memory requirements** allow for the easy integration of Node.js as software into single-board controllers such as Arduino, widely used for building digital devices that make up IoT systems. Finally, the Node community has been an early adopter of the IoT technology, creating over 80 packages for Arduino controllers and multiple packages for the Pebble and Fitbit wearable devices widely used in IoT systems.

Node.js **offers fewer abstractions** than for example ASP.NET, allowing developers to **write code using a multitude of small components** rather than configuring a vast number of parameters.

Node.js will prove **useful in situations when something faster and more scalable than Rails is needed**.

The Node.js developers **community is a very active and vibrant group **of developers who contribute to constant improvement of Node.js.

## Cons

Node.js is **not so good for developing CPU-intensive** applications that involve the generation and processing of images, audio, or video. **Being a single-threaded solution, Node.js may be become unresponsive and slow in processing large files.** In this case, conventional multi-threaded solutions will be your best bet.
> So just spawn workers, well! That's the whole deal with Node.js. Heavy stuff can run in another process, and you process it's results in a lightweight callback.
> [https://stackoverflow.com/questions/17959663/why-is-node-js-single-threaded#comment26250255_17959746](https://stackoverflow.com/questions/17959663/why-is-node-js-single-threaded#comment26250255_17959746)> Converting product data into a UI is not CPU intensive, nor is calculating orders or the like. Most of the web is pretty transactional. CPU intensive stuff is things like converting videos, converting image formats, etc. Much of that is due to file i/o which, actually, node does pretty well. And makes it **easy to offload to another process that's dedicated to the converting**.
> [https://stackoverflow.com/questions/17959663/why-is-node-js-single-threaded#comment26252014_17959746](https://stackoverflow.com/questions/17959663/why-is-node-js-single-threaded#comment26252014_17959746)

Node.js is **not best choice for applications with a vast code** **base** – since Java provides strongly typed sources, refactoring it and bug fixing will be more straightforward during its maintenance.

## Infra

Node.js **works perfectly with the leading cloud computing tools**, keeps the infrastructure costs under control, and **gives you access to the best services that predict usage spikes, expand resources and control the development process**.

With AWS and Node.js you get a set of development tools that can predict and detect an increase in web application traffic and usage to automatically add virtual machines to meet the new requirements.

### SERVERLESS

Node.js **allows for serverless app development**. The easiest way to do it is to use the **Serverless framework** powered by AWS. You can build apps directly in the AWS environment. All the processes take place there, so you don't need DevOps, because everything is configured automatically. Your app's developer writes code, uploads it to Serverless, and it’s all set up.

### MICROSERVICES

Node.js **is an excellent pick for the microservices architecture approach**, which offers excellent scalability and stability.

Node.js with microservices significantly reduces application deployment time and **enhances efficiency, maintainability, and scalability of your applications**.

Using microservices, you **build your app from separate small blocks that perform one function** (e.g., checkout in an e-commerce app, product page, shopping cart, etc). Each block receives information, computes it, and delivers the result. **You can add, multiply, and remove these elements according to your needs.** **This brings stability. **First of all, if one element crashes, for instance, the checkout, the users who are browsing the other parts of the store will not notice it.

Building software with a microservices architecture is fast and easy, however, if you include too many blocks and too many relations among them, **supporting and expanding such an architecture may become tricky when you put dozens of element together**.

### EXAMPLES

PayPal, a worldwide online payments system, has also moved their backend development from Java to JavaScript and Node.js. Beforehand, the engineering teams at the company were divided into those who code for the browser and those who code for the application layer, and it didn’t work perfectly. Then, full-stack engineers came to the rescue, but that model wasn’t ideal too. Adopting Node.js solved their problems, as it allowed for writing the browser and the server applications in the same programming language – JavaScript. As a result, the unified team is able to understand problems at both ends and react more effectively to the customer needs. Read more here about how smaller Node.js team started work 2 months after bigger Java team and catched them up: [https://www.paypal-engineering.com/2013/11/22/node-js-at-paypal/](https://www.paypal-engineering.com/2013/11/22/node-js-at-paypal/)

### Sources

*   [https://medium.com/paypal-engineering/node-js-at-paypal-4e2d1d08ce4f](https://medium.com/paypal-engineering/node-js-at-paypal-4e2d1d08ce4f)
*   [https://www.netguru.com/hs-fs/hubfs/Blog_posts_-_images/image1-15.png?width=980&amp;height=755&amp;name=image1-15.png](https://www.netguru.com/hs-fs/hubfs/Blog_posts_-_images/image1-15.png?width=980&amp;height=755&amp;name=image1-15.png)
*   [https://www.netguru.com/blog/top-companies-used-nodejs-production](https://www.netguru.com/blog/top-companies-used-nodejs-production)
*   [https://www.netguru.com/blog/node.js-scalability-how-your-web-application-can-benefit-from-node.js](https://www.netguru.com/blog/node.js-scalability-how-your-web-application-can-benefit-from-node.js)
*   [https://www.netguru.com/blog/node.js-vs.-asp.net-for-enterprise-solutions-which-stack-to-choose-for-advanced-web-applications](https://www.netguru.com/blog/node.js-vs.-asp.net-for-enterprise-solutions-which-stack-to-choose-for-advanced-web-applications)
*   [https://www.netguru.com/blog/pros-cons-use-node.js-backend](https://www.netguru.com/blog/pros-cons-use-node.js-backend)
*   [https://www.netguru.com/blog/use-node-js-backend](https://www.netguru.com/blog/use-node-js-backend)

# Advantages of development in Node.js

*   **Serialization** - in Node.js mostly builtin, we use `response.json()` or `json.stringify()`
*   `schema` - joi, parsing and validation of form values, parsing and validation of query string, schm, ajv, [https://scotch.io/tutorials/node-api-schema-validation-with-joi](https://scotch.io/tutorials/node-api-schema-validation-with-joi)
*   Very solid article about Node.js backend that uses TypeScript, TypeORM, SQL database, Winston logger, PM2 process manager, Redis: [https://itnext.io/production-ready-node-js-rest-apis-setup-using-typescript-postgresql-and-redis-a9525871407](https://itnext.io/production-ready-node-js-rest-apis-setup-using-typescript-postgresql-and-redis-a9525871407)
*   PM2 process manager or Rollbar help detect and track errors easily, boosting developers' productivity