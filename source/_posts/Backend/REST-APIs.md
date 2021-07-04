---
title: 'REST APIs'
tags:
  - Backend
  - REST APIs
categories:
  - [Backend]
date: 2021-07-04
---
# REST APIs
* GET, POST (/book), DELETE, PUT (/book/:id) to perform CRUD
* detailed explanation:
  * POST (create a resource or generally provide data)
  * GET (retrieve an index of resources or an individual resource)
  * PUT (create or replace a resource) - you send whole object to change
  * PATCH (update/modify a resource) - you send only specific properties to change
  * DELETE (remove a resource)
* sample paths:
  * [POST] endpoint/users
  * [GET] endpoint/users (list users)
  * [GET] endpoint/users/:userId (get specific user)
  * [PATCH] endpoint/users/:userId (update the data for the specified user)
  * [DELETE] endpoint/users/:userId (remove the specified user)
  * [GET] `/users/:userId/books/:bookId`
  ```
  Route path: /flights/:from-:to
  Request URL: http://localhost:3000/flights/LAX-SFO
  req.params: { "from": "LAX", "to": "SFO" }
  ```