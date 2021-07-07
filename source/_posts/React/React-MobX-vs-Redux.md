---
title: MobX vs Redux
tags:
  - React
  - MobX
  - Redux
  - React state management
categories:
  - [React, State management]
date: 2020-07-17 21:25:00
---
- MobX diagram: https://camo.githubusercontent.com/c8e97f5bf3e6908e68b34fd187d97fac599afc4efc2807a3434782285db46357/68747470733a2f2f6d6f62782e6a732e6f72672f6173736574732f666c6f77322e706e67
- MobX Github: https://github.com/mobxjs/mobx
- Flux vs Redux: https://cdn-images-1.medium.com/max/1600/1*3lvNEQE4SF6Z1l-680cfSQ.jpeg
- When To Add Redux: https://daveceddia.com/what-does-redux-do/
- Why Redux adds some complexity to your application: https://www.quora.com/Do-I-need-Redux

## Attributes
- these two are state management libraries
- Redux has **single store**, Mobx can have **multiple stores**
- Redux uses **normal objects**, Mobx uses **observables**
  - You can listen to an observable and automatically track changes that occur to the data
  - In Redux all the updates have to be tracked manually by proper functions
- Redux has **immutable state**, state is read-only and is pure
  - In Redux it's easy to revert back to a previous state. Eg — An undo action.
- MobX can have state overwritten (**mutable state**)
- MobX is much easier to learn and has a steady learning curve
- Redux follows **functional** programming paradigm
- MobX **functional reactive** programming
- In MobX there is lot of built in **abstraction**, and this leads to less code
- When implementing **Redux** you will end up writing **lot of boilerplate code**
- Since there is more abstraction, **debugging becomes a lot harder for MobX**
- Redux provides kickass **developer tools including time travelling**
- With **pure functions and less abstraction, debugging in Redux will be a better experience** compared to MobX
- Following the flux paradigm makes Redux more predictable
- Because of the whole pure functions things and functional programming paradigm **Redux is more maintainable**
- The developer community of Redux is way ahead of the MobX community
- **MobX is great for small and simple apps**
- It's faster to build apps with MobX
- Redux allows to create more maintainable code
- For **complex app with scalable option Redux is great choice**