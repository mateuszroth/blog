---
title: '[DRAFT] Node.js notes'
tags:
  - Backend
  - Node.js
categories:
  - [Node.js, Basics]
date: 2019-01-01 10:00:00
---

# TODO

*   go through some articles [https://medium.com/@pankaj.panigrahi/list-of-node-js-articles-ededa6dd304b](https://medium.com/@pankaj.panigrahi/list-of-node-js-articles-ededa6dd304b)
*   go through ACL / Roles and permissions

### Libraries for automatically parsing the data, most commonly through middlewares

querystring, body, and cookies parsing

# ACL / Roles and permissions

TODO:

*   [https://stackoverflow.com/questions/38893178/what-is-the-best-way-to-implement-roles-and-permission-in-express-rest-api](https://stackoverflow.com/questions/38893178/what-is-the-best-way-to-implement-roles-and-permission-in-express-rest-api)
*   [https://gist.github.com/facultymatt/6370903](https://gist.github.com/facultymatt/6370903)
*   [https://www.npmjs.com/package/accesscontrol](https://www.npmjs.com/package/accesscontrol)

# Token/JWT Authentication

## Authorization header

Example header is as below:

`Authorization: Bearer a1194981-b541-416e-935`

The header field should be “Authorization” and the first part of the value should be the keyword “Bearer” and then the second part separated by a space should contain the token.

This is a standard given by W3C. The keyword “Bearer” was used to distinguish this from the existing Basic auth.

# API Key validation

Simple example by using a dedicated api key header: [https://medium.com/better-programming/getting-data-from-mongodb-creating-an-api-key-validation-middleware-in-express-944382205d3e](https://medium.com/better-programming/getting-data-from-mongodb-creating-an-api-key-validation-middleware-in-express-944382205d3e)

# Elasticsearch

In theory: [https://medium.com/better-programming/introduction-to-elasticsearch-using-node-js-part-1-164311327557](https://medium.com/better-programming/introduction-to-elasticsearch-using-node-js-part-1-164311327557)

In practice in Node.js:
[https://medium.com/better-programming/introduction-to-elasticsearch-using-node-js-part-2-4c804427bc94](https://medium.com/better-programming/introduction-to-elasticsearch-using-node-js-part-2-4c804427bc94)

Elasticsearch course on Udemy to buy and watch:
[https://www.udemy.com/course/elasticsearch-complete-guide/](https://www.udemy.com/course/elasticsearch-complete-guide/)