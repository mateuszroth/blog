---
title: React - miscellaneous notes
tags:
  - React
categories:
  - [React, Basics]
date: 2019-12-01
---
# General notes
## Hints
* treat components like pure functions and don't modify props

# Terms

## Reconcililation
[https://reactjs.org/docs/reconciliation.html](https://reactjs.org/docs/reconciliation.html)

* React implements a heuristic O(n) algorithm to compare rendered tree nodes
* Two elements of different types will produce different trees
* The developer can hint at which child elements may be stable across different renders with a `key` prop
* When a component updates, the instance stays the same, so that state is maintained across renders
* Keys should be stable, predictable, and unique. Unstable keys (like those produced by `Math.random()`) will cause many component instances and DOM nodes to be unnecessarily recreated, which can cause performance degradation and lost state in child components

## Prop drilling

Passing props through a component tree, not a good pattern in most cases:

[Props drilling example](https://miro.medium.com/max/2052/1*p_K7-j3GUX3A1XSzaFo0fQ.png)

<img src="https://miro.medium.com/max/2052/1*p_K7-j3GUX3A1XSzaFo0fQ.png" width="400"/>

## Context

Context is a way to essentially create global variables that can be passed around in a React app so no prop drilling would be needed.

Context is often touted as a **simpler, lighter solution to using Redux** for state management.

# Testing
## Snapshot testing

* To make our tests really useful, we should run them before each commit. So we can be sure, that we didn’t break anything accidentally. For example [_<em>husky_</em>](https://www.npmjs.com/package/husky) package can help to setup and run pre-commit hooks.
* The snapshot tests become really powerful when you are working on larger application or multiple developers are working on the same codebase.
* Life examples when snapshot tests fail are available here in the section "Typical regressions": [https://medium.com/simply/snapshots-painless-testing-of-react-components-6bce3c4d51fc](https://medium.com/simply/snapshots-painless-testing-of-react-components-6bce3c4d51fc)
