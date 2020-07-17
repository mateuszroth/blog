---
title: 'CSS - How to make child div wider than parent div'
tags:
  - Frontend
  - CSS
categories:
  - [Frontend, CSS]
date: 2020-07-17 20:00:00
---
## By using `calc`
[Source](https://stackoverflow.com/a/24895631)
```css
html,
.parent {
    height: 100%;
    width: 100%;
    text-align: center;
    padding: 0;
    margin: 0;
}
.parent {
    width: 50%;
    max-width: 800px;
    background: grey;
    margin: 0 auto;
    position: relative;
}
.child-element {
    position: relative;
    width: 100vw;
    left: calc(-50vw + 50%);
    height: 50px;
    background: blue;
}
```

## How do we make a full-browser-width container when we're inside a limited-width parent?
[Source](https://css-tricks.com/full-width-containers-limited-width-parents/)
```css
.full-width {
  width: 100vw;
  position: relative;
  left: 50%;
  right: 50%;
  margin-left: -50vw;
  margin-right: -50vw;
}
```