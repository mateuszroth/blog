---
title: 'Reason programming language attributes'
tags:
  - Software Engineering
  - Programming languages
  - Reason
categories:
  - [Software Engineering, Programming languages]
date: 2020-07-17 20:00:00
---
## How to start React project in Reason: 
- https://blog.pusher.com/reason-react-bucklescript/
- https://blog.pusher.com/react-vs-reasonreact/
- https://blog.pusher.com/reason-javascript/

## Variants
*Variants* in Reason are data types and structures. It can be used to define sets of symbols and data structures.
`type animal = Cat(string) | Dog(string);`

## Functions
*Functions* in Reason are declared with an arrow and a return expression.
```reason
let speak = (animal) =>
  switch (animal) {
  | Cat(name) => name ++ " says: meow"
  | Dog(name) => name ++ " says: woof"
};
```

## React
A React `component` can either be stateless or stateful. In `ReasonReact`, there are different ways of defining them:
- Stateless components: defined as `ReasonReact.statelessComponent("componentName")`
- Stateful components: defined as `ReasonReact.reducerComponent("componentName")`

`let make = (~message, _children) => {`
The first parameter has a symbol ~ indicating that it was passed into the App component as a props and the second parameter has _, this is a more explicit way of showing that the parameter isn’t used and ignored.