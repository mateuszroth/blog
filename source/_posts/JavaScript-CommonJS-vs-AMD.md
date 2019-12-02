---
title: JavaScript CommonJS vs AMD
tags:
  - JavaScript
categories:
  - [JavaScript, Basics]
date: 2019-09-22 18:17:59
---

# CommonJS

* uses `exports` and `require` keywords
* needs module identifier
* not designed for browser
* Browserify will let you use CommonJS in the browser
* CommonJS `require()` is a synchronous call, it is expected to return the **module immediately** which does not work well in the browser
* Node.js and RingoJS are server-side JavaScript runtimes, and yes, both of them implement modules based on the CommonJS Module spec

# AMD

* `RequireJS` implements it
* suits web browser envs
* **supports asynchronous loading** of module dependencies
* `define` keyword
* example:
```js
  define('module/id/string', ['module', 'dependency', 'array'], 
    function(module, factory function) {
      return ModuleContents;  
  });
```