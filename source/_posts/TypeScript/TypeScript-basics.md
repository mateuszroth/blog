---
title: TypeScript basics
tags:
  - JavaScript
  - TypeScript
categories:
  - [JavaScript, TypeScript]
date: 2019-12-01 16:13:00
---

## ! operator

```js
if (a!.b!.c) { }
```

compiles to JS:

```js
if (a.b.c) {
}
```

## ? operator

```js
let x = foo?.bar.baz();
```

compiles to JS:

```js
let x = foo === null || foo === undefined ? undefined : foo.bar.baz();
```

And:

```js
if (someObj?.bar) {
  // ...
}
```

is equivalent in JS to:

```js
if (someObj &amp;&amp; someObj.someProperty) {
    // ...
}
```

TS:

```js
interface Content {
  getUrl?: () => string;
  url?: string;
}
interface Data {
  content?: Content;
}
let data: Data | undefined;
const url: string | undefined = data?.content?.getUrl?.();
const url2: string | undefined = data?.content?.url;
```