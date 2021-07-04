---
title: 'HTTP'
tags:
  - Backend
  - HTTP
categories:
  - [Backend]
date: 2021-07-04
---
# HTTP
## HTTP 2.0: **multiplexing, server push, header compression**
* In particular, HTTP/2 is much faster and more efficient than HTTP/1.1
* In HTTP/2, developers have hands-on, detailed **control over prioritization**. This allows them to maximize perceived and actual page load speed to a degree that was not possible in HTTP/1.1
* HTTP/2 is **multiplexed, i.e., it can initiate multiple requests in parallel over a single TCP connection**. As a result, web pages containing several elements are delivered over one TCP connection. These capabilities solve the head-of-line blocking problem in HTTP/1.1, in which a packet at the front of the line blocks others from being transmitted.
* HTTP/2 uses **header compression** to reduce the overhead caused by TCP’s slow-start mechanism.
* As opposed to HTTP/1.1, which keeps all requests and responses in plain text format, **HTTP/2 uses the binary framing layer to encapsulate all messages in binary format**, while still maintaining HTTP semantics, such as verbs, methods, and headers.
* HTTP/2 **allows a server to "push" content** to a client before the client asks for it. 
* **HTTP/3 runs over QUIC instead of TCP**. QUIC is a faster and more secure transport layer protocol that is designed for the needs of the modern Internet.