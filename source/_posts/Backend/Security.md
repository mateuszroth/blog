---
title: 'Security'
tags:
  - Backend
  - Security
categories:
  - [Backend]
date: 2021-07-04
---
# Security

* **File inclusion vulnerability** - doesn't upload files like .exe or some scripts than can be accidentally run on server
* **SQL injection** - clean user input
* **CSRF (Cross site request forgery)** and cookies
  * In a cross-site request forgery attack, the attacker tries to force/trick you into making a request which you did not intend. This could be sending you a link that makes you involuntarily change your password. A malicious link could look like that: `https://security.stackexchange.com/account?new_password=abc123`
  * **The browser automatically sending cookies also has a big downside, which is CSRF attacks**. In a CSRF attack, a malicious website takes advantage of the fact that your **browser will automatically attach authentication cookies to requests** to that domain and tricks your browser into executing a request.
  * cookies make it more difficult for non-browser based applications (like mobile to tablet apps) to consume your API.
  * JWTs are stored as cookies on many occasions, and cookies are vulnerable/susceptible to CSRF (Cross-site Request Forgery) attacks. One of the many ways **to prevent CSRF attacks is to ensure that your cookie is accessible by only your domain**. As a developer, ensure that necessary CSRF protections are put in place to avoid these attacks, regardless of the use of JWTs.
* **XSS**
  * In a **cross-site scripting attack**, the attacker makes you involuntarily execute client-side code, most likely Javascript. A typical reflected XSS attacking attempt could look like this: `https://security.stackexchange.com/search?q="><script>alert(document.cookie)</script>`
  * (Cross-site scripting): an attacker embeds a script in the victim site (**the victim site is only vulnerable if inputs are not sanitized correctly**), and the attacker's script can do anything JavaScript is allowed to do on the page.
  * **If you store JWT tokens in local storage, the attacker's script could read those tokens, and also send those tokens to a server they control**. In fact, a lot of people advocate that very sensitive data shouldn’t be stored in Web Storage because of XSS attacks
