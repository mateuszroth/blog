---
title: '[DRAFT] React rendering and reconciliation algorithm'
tags:
  - React
categories:
  - [React, Basics]
date: 2019-01-01 10:00:00
---

[https://reactjs.org/docs/reconciliation.html](https://reactjs.org/docs/reconciliation.html)

*   React implements a heuristic O(n) algorithm to compare rendered tree nodes
*   Two elements of different types will produce different trees
*   The developer can hint at which child elements may be stable across different renders with a `key` prop
*   When a component updates, the instance stays the same, so that state is maintained across renders
*   Keys should be stable, predictable, and unique. Unstable keys (like those produced by `Math.random()`) will cause many component instances and DOM nodes to be unnecessarily recreated, which can cause performance degradation and lost state in child components