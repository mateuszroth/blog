---
title: JavaScript - `parseInt` vs `Number` comparision
tags:
  - JavaScript
categories:
  - [JavaScript, Basics]
date: 2019-07-05 23:00:00
---

<!--kg-card-begin: code-->

    parseInt(string, radix);

    var a = new Number('123'); // a === 123 is false
    var b = Number('123'); // b === 123 is true
<!--kg-card-end: code-->

*   `parseInt` takes 2 arguments

`Number`:

*   returns `NaN` for string `123sdfdsf`
*   returns `NaN` for `undefined`, `NaN` and `{}`
*   returns `0` for `false`, `null`, `""`, `" "`
*   returns `1` for `true`

`parseInt`:

*   returns `123` for string `123sdfdsf`
*   returns `NaN` for all `false`, `null`, `""`, `" "`, `true`, `{}`, `undefined` and `NaN`
*   `parseInt` preferable for inputs where user can leave some additional characters