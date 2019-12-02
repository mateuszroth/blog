---
title: JavaScript - performance / time measurement of function calls
tags:
  - JavaScript
categories:
  - [JavaScript, Performance]
date: 2019-09-22 18:13:48
---

You can use `performance.now()`:
<!--kg-card-begin: code-->

    const t0 = performance.now();
    const arr1 = [1, 2, 3, 4, 5];
    arr1.unshift(0);
    const t1 = performance.now();
    console.log(t1 - t0);

    const t2 = performance.now();
    const arr2 = [1, 2, 3, 4, 5];
    const arr3 = [0, ...arr2];
    const t3 = performance.now();
    console.log(t3 - t2);
    `</pre><!--kg-card-end: code-->

    Or `console.time` and `console.timeEnd`:
    <!--kg-card-begin: code--><pre>`console.time('unshift');
    const arr1 = [1, 2, 3, 4, 5];
    arr1.unshift(0)
    console.timeEnd('unshift');

    console.time('destructuring');
    const arr2 = [1, 2, 3, 4, 5];
    const arr3 = [0, ...arr2];
    console.timeEnd('destructuring');
<!--kg-card-end: code-->