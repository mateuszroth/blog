---
title: 'Message brokers'
tags:
  - Backend
  - RabbitMQ
categories:
  - [Backend]
date: 2021-07-05
---
# Message brokers
* a message broker accepts and forwards messages
* allows applications to communicate via a queuing mechanism
* a program that sends messages is a *producer*
* a *queue* is essentially a large message buffer
* many *producers* can send messages that go to one *queue*, and many *consumers* can try to receive data from one *queue*
* a *consumer* is a program that mostly waits to receive messages

## Use cases
* Point-to-point messaging
* Publish/subscribe - event-driven architecture-based system, where applications have fewer dependencies between each other
* Long-running tasks and crucial API like preparing files to download
* Microservices - to create event-based communication and use the message broker together with publish/subscribe pattern instead of REST APIs
* Transactional systems - where we have several actions that need to be made after each previous one completes

## Advantages
* Improved system performance by introducing asynchronous processing
* Increased reliability by guaranteeing the transmission of messages
  * In case of consumer failure, it can redeliver the message immediately or after some specified time

## Disadvantages
* Increased system complexity
  * maintaining the network between components or security issues
  * problem related to eventual consistency where some components could not have up-to-date data until the messages are propagated and processed
* Debugging can be harder
* There’s a steep learning curve at first
  * size of queues and messages, the behavior of queues, delivery settings or messages TTL

## Amazon SQS & SNS
* you can combine Amazon SNS power of publishing to multiple recipients with Amazon SQS durable queues

## Examples
* (tutorial for Node.js using amqp and RabbitMQ)[https://www.rabbitmq.com/tutorials/tutorial-one-javascript.html]
* (tutorial for Node.js using amqplib and RabbitMQ)(https://medium.com/swlh/communicating-using-rabbitmq-in-node-js-e63a4dffc8bb)

## Sources 
* https://www.rabbitmq.com/tutorials/tutorial-one-javascript.html
* https://tsh.io/blog/message-broker/
* https://blog.logrocket.com/understanding-message-queuing-systems-using-rabbitmq/