---
title: React - miscellaneous notes
tags:
  - React
categories:
  - [React, Basics]
date: 2019-12-01 17:55:26
---
# Terms

## Prop drilling

Passing props through a component tree, not a good pattern in most cases:

[Props drilling example](https://miro.medium.com/max/2052/1*p_K7-j3GUX3A1XSzaFo0fQ.png)

<img src="https://miro.medium.com/max/2052/1*p_K7-j3GUX3A1XSzaFo0fQ.png" width="400"/>

## Context

Context is a way to essentially create global variables that can be passed around in a React app so no prop drilling would be needed.

Context is often touted as a **simpler, lighter solution to using Redux** for state management.

# Snapshot testing

*   To make our tests really useful, we should run them before each commit. So we can be sure, that we didn’t break anything accidentally. For example [_<em>husky_</em>](https://www.npmjs.com/package/husky) package can help to setup and run pre-commit hooks.
*   The snapshot tests become really powerful when you are working on larger application or multiple developers are working on the same codebase.
*   Life examples when snapshot tests fail are available here in the section "Typical regressions": [https://medium.com/simply/snapshots-painless-testing-of-react-components-6bce3c4d51fc](https://medium.com/simply/snapshots-painless-testing-of-react-components-6bce3c4d51fc)

# Higher Order Components

## Comparison to Render Props and React Hooks:

[https://medium.com/simply/comparison-hocs-vs-render-props-vs-hooks-55f9ffcd5dc6](https://medium.com/simply/comparison-hocs-vs-render-props-vs-hooks-55f9ffcd5dc6)

## HOCs pitfalls

### Don’t Use HOCs Inside the render Method

Apply HOCs outside the component definition so that the resulting component is created only once. Then, its identity will be consistent across renders. This is usually what you want, anyway.

Docs: [https://reactjs.org/docs/higher-order-components.html#dont-use-hocs-inside-the-render-method](https://reactjs.org/docs/higher-order-components.html#dont-use-hocs-inside-the-render-method)

### Class Static Methods Must Be Copied Over

Docs: [https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)

When you use HOC or just wrap a component by a function, static methods are not being exposed by that HOC/function:

```javascript
// Define a static method
WrappedComponent.staticMethod = function() {/*...*/}
// Now apply a HOC
const EnhancedComponent = enhance(WrappedComponent);

// The enhanced component has no static method
typeof EnhancedComponent.staticMethod === 'undefined' // true
```

How to solve: [https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)

### Refs Aren’t Passed Through

If you add a ref to an element whose component is the result of a HOC, the ref refers to an instance of the outermost container component, not the wrapped component.

How to solve: [<a href="https://reactjs.org/docs/higher-order-components.html#refs-arent-passed-through">https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)</a>

## Types of HOCs

* **Enhancers**: Wrap a component with additional functionality/props.
* **Injectors**: Inject props into a component.
* Recommended article about: [https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb](https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb)

# Render Props

## Issues of

* Firstly, there is an **issue with separation of concerns** with Render Props; if you wrap a component with a render prop in the same component, it will make it more difficult to test the two in isolation. May be fixed by creating more boilerplate code and creating separate component for what is rendered inside the render prop
* Secondly, as the props are injected in the render function of component, you cannot make use of them in the lifecycle methods
* Source: [https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c](https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c)

## Render Prop vs HOC

* In the end, the tradeoff between HOCs and render prop components comes down to **flexibility vs convenience**. This can be solved by writing render prop components first, then generating HOCs from them, which gives the consumer the power to choose between the two.
* As far as TypeScript goes, there is no doubt that typing HOCs is much more difficult.
* Prior to React v16.8.0, I’d recommend **sticking with render prop components for the flexibility and simplicity of typing**, and if the need arises, such as building a reusable library of components, or for render prop components that are simple and/or widely used across a project, I would only then generate a HOC from them.
* in React v16.8.0, I would strongly recommend using them over both higher-order components or render props where possible, as they are much simpler to type.
* Source: [https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c](https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c)

# React Hooks

## FAQ

* [Is there something like class instance variables so we won't need to use state and rerender component?](https://reactjs.org/docs/hooks-faq.html#is-there-something-like-instance-variables)

## Hook as HOC
```javascript
import React, { useState, useEffect } from "react";

function useDataFetching(dataSource) {
  const [loading, setLoading] = useState(true);
  const [results, setResults] = useState([]);
  const [error, setError] = useState("");

  useEffect(() =>
   {
    async function fetchData() {
      try {
        const data = await fetch(dataSource);
        const json = await data.json();

        if (json) {
          setLoading(false);
          setResults(json);
        }
      } catch (error) {
        setLoading(false);
        setError(error.message);
      }

      setLoading(false);
    }

    fetchData();
  }, [dataSource]);

  return {
    error,
    loading,
    results
  };
}

export default useDataFetching;
```
Data Fetching HOC as React Hooks, source [https://dev.to/gethackteam/from-higher-order-components-hoc-to-react-hooks-2bm9](https://dev.to/gethackteam/from-higher-order-components-hoc-to-react-hooks-2bm9)

Source and comparison to standard HOC: [https://dev.to/gethackteam/from-higher-order-components-hoc-to-react-hooks-2bm9](https://dev.to/gethackteam/from-higher-order-components-hoc-to-react-hooks-2bm9)

## Use only Hooks for global state management

You can use `useContext` and `useReducer` to create a Redux-like store management in your app. Checkout [https://medium.com/simply/state-management-with-react-hooks-and-context-api-at-10-lines-of-code-baf6be8302c](https://medium.com/simply/state-management-with-react-hooks-and-context-api-at-10-lines-of-code-baf6be8302c)
```javascript
import { StateProvider } from '../state';

const App = () =>
 {
  const initialState = {
    theme: { primary: 'green' }
  };

  const reducer = (state, action) =>
   {
    switch (action.type) {
      case 'changeTheme':
        return {
          ...state,
          theme: action.newTheme
        };

      default:
        return state;
    }
  };

  return (
    <StateProvider initialState={initialState} reducer={reducer}>
        // App content ...
    </StateProvider>
  );
}
```
usage
```js
import { useStateValue } from './state';

const ThemedButton = () => {
  const [{ theme }, dispatch] = useStateValue();
  return (
    <Button
      primaryColor={theme.primary}
      onClick={() => dispatch({
        type: 'changeTheme',
        newTheme: { primary: 'blue'}
      })}
    >
      Make me blue!
    </Button>
  );
}
```
