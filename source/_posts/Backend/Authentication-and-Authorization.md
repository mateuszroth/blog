---
title: 'Authentication and Authorization'
tags:
  - Backend
  - Authorization
  - Authentication
categories:
  - [Backend]
date: 2021-07-04
---
# Authentication and Authorization
* **Authentication** (pl. *uwierzytelnianie, autentykacja*) describes the process of claiming an identity. That’s what you do when you log in to a service with a username and password, you authenticate yourself.
* **Authorization** on the other hand describes permission rules that specify the access rights of individual users and user groups to certain parts of the system, i.e. ACL.
* In modern era, everyone is going for token based authentication instead of session based cookies.
* A spreadsheet describing authentication techniques: (Authentication Techniques for APIs)[https://docs.google.com/spreadsheets/d/1tAX5ZJzluilhoYKjra-uHbMCZraaQkqIHl3RIQ8mVkM/edit#gid=0]

## Authentication
* When we do token-based authentication, such as OpenID, OAuth, or OpenID Connect, we receive an `access_token` (and sometimes `id_token`) from a trusted authority
* Passport is an authentication middleware for Node.js
  * Packages
    * `bcrypt` for hashing user passwords
    * `jsonwebtoken` for signing tokens
    * `passport-local` for implementing local strategy
    * `passport-jwt` for retrieving and verifying JWTs

### OAuth2
* i.e. Facebook, Google
* You need to register your app on authorization server such as Google. You will get `client id` for your app, you will have defined both `redirect URL` and `client secret`.
* The `redirect URL` is used by the authorization server after an user logs in successfully to the server.
* Sample steps:
  1. To get authorization code user calls authorization server https://cloud.digitalocean.com/v1/oauth/authorize?response_type=code&client_id=CLIENT_ID&redirect_uri=CALLBACK_URL&scope=read
  2. Send authorization code to our app https://dropletbook.com/callback?code=AUTHORIZATION_CODE
  3. After receiveing authorization code, our app calls authorization server to get access token https://cloud.digitalocean.com/v1/oauth/token?client_id=CLIENT_ID&client_secret=CLIENT_SECRET&grant_type=authorization_code&code=AUTHORIZATION_CODE&redirect_uri=CALLBACK_URL
  4. Our app gets access token `{"access_token":"ACCESS_TOKEN","token_type":"bearer","expires_in":2592000,"refresh_token":"REFRESH_TOKEN","scope":"read","uid":100101,"info":{"name":"Mark E. Mark","email":"mark@thefunkybunch.com"}}`
* visual explanation: https://darutk.medium.com/the-simplest-guide-to-oauth-2-0-8c71bd9a15bb
* another explanation for steps:
  1. User wants to request a resource that requires auth
  2. Authorization server returns an *authorization code* to the client
  3. Client then uses that *authorization code* in order to request an *authorization token* - e.g. a JWT


### Scalability of token/cookie based authentication
* in horizontal scaling scenario you have to start replicating servers
  * for **cookie based authentication has a disadvantage of need for central session storage system** that all of your application servers have access to
    * Setting up and maintaining this type of distributed system involves in-depth technical knowledge and subsequently **incurs higher financial costs**
  * for **JWT based authentication our application can scale easily** because we can use tokens to access resources from different servers without worrying if the user was actually logged in on a particular server. You also save costs because you don’t need a dedicated server to store your sessions. Why? Because there are no sessions!

## Authorization
### JWT (JSON Web Tokens)
* JSON Web Token (JWT) is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.
* JWTs can be signed using a secret (with HMAC algorithm) or a public/private key pair using RSA.
* JWTs consist of three parts separated by dots (.), which are:
  * Header
    * consists of two parts: the type of the token, which is JWT, and the hashing algorithm such as HMAC SHA256 or RSA
    * JSON is encoded to Base64Url
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
  * Payload
    * The payload contains all the required information about the user
    * do not store passwords here or secret data
```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```
  * Signature
    * you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that to create signature
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```
* can be sent through an URL, POST parameter, or inside an HTTP header
* JWT sent over as an `Authorization: Bearer <token>` header is a stateless authentication mechanism as the user state is never saved in the server memory

#### Advantages
* They are easy to scale horizontally
* due to its size its transmission is fast
* They are easier to maintain and debug
* They have the ability to create truly RESTful Services
* They have built-in expiration functionality
* JSON Web Tokens are self-contained
* JWT is a **stateless authentication** mechanism as the user state is never saved in the server memory
* doesn’t matter which domains are serving your APIs, as **Cross-Origin Resource Sharing (CORS) won’t be an issue** as it doesn’t use cookies
* a good way of securely transmitting information between parties

#### Disadvantages
* (Why JWTs Suck as Session Tokens)[https://developer.okta.com/blog/2017/08/17/why-jwts-suck-as-session-tokens]

#### Precautions
* a great care must be taken to prevent security issues and you **should not keep tokens longer than required**
* **you also should not store sensitive session data in browser storage due to lack of security**

#### Invalidation
* Simply remove the token from the client
* Create a token blocklist or whitelist
* Just keep token expiry times short and rotate them often

#### While using cookies
* Cookies/session id is not self contained. It is a reference token. During each validation the Gmail server needs to fetch the information corresponding to it.
  * Cookie/session based authentication doesn't scale well
* JWT is self contained. It is a value token. So during each validation the Gmail server does not needs to fetch the information corresponding to it. It is most suitable for Microservices Architecture
  * with JWTs REST API is stateless and therefore without side effects means that maintainability and debugging are made much easier
  * CORS - for an API to be served from one server and for the actual application to consume it from another. To make this happen, we need to enable Cross-Origin Resource Sharing (CORS). Since cookies can only be used for the domain from which they originated, they aren’t much help for APIs on different domains than the application. Using JWTs for authentication in this case ensures that the RESTful API is stateless

#### Use cases
* Authorization: This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.

### ACL / Roles and permissions
* [Permissions should be handled by defining specific user roles with their access control lists](https://stackoverflow.com/questions/38893178/what-is-the-best-way-to-implement-roles-and-permission-in-express-rest-api)
* [`node_acl`](https://github.com/OptimalBits/node_acl) package
* [`accesscontrol`](https://www.npmjs.com/package/accesscontrol) package

## Sources
* https://auth0.com/learn/json-web-tokens/
* https://betterprogramming.pub/authentication-and-authorization-using-redis-49c5f0e6b311