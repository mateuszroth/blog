---
title: 'Authentication and Authorization'
tags:
  - Backend
  - Authorization
  - Authentication
categories:
  - [Backend, Authentication, Authorization]
date: 2021-07-04
---
# Authentication and Authorization
• **Authentication** (pl. *uwierzytelnianie, autentykacja*) describes the process of claiming an identity. That’s what you do when you log in to a service with a username and password, you authenticate yourself.
• **Authorization** on the other hand describes permission rules that specify the access rights of individual users and user groups to certain parts of the system, i.e. ACL.

## Authentication
* When we do token-based authentication, such as OpenID, OAuth, or OpenID Connect, we receive an `access_token` (and sometimes `id_token`) from a trusted authority

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
* JWT sent over as an `Authentication Bearer` header is a stateless authentication mechanism as the user state is never saved in the server memory

#### Advantages
* They are easy to scale horizontally
* due to its size its transmission is fast
* They are easier to maintain and debug
* They have the ability to create truly RESTful Services
* They have built-in expiration functionality
* JSON Web Tokens are self-contained
* a good way of securely transmitting information between parties

#### Invalidation
* Simply remove the token from the client
* Create a token blocklist or whitelist
* Just keep token expiry times short and rotate them often

#### Use cases
* Authorization: This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.

#### Sources
* https://auth0.com/learn/json-web-tokens/


### ACL / Roles and permissions
#### TODO:
* [https://stackoverflow.com/questions/38893178/what-is-the-best-way-to-implement-roles-and-permission-in-express-rest-api](https://stackoverflow.com/questions/38893178/what-is-the-best-way-to-implement-roles-and-permission-in-express-rest-api)
* [https://gist.github.com/facultymatt/6370903](https://gist.github.com/facultymatt/6370903)
* [https://www.npmjs.com/package/accesscontrol](https://www.npmjs.com/package/accesscontrol)