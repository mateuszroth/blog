---
title: React - code reusability
tags:
  - React
categories:
  - [React, Basics]
date: 2021-07-06
---
# Code reusability
## Higher Order Components

### Comparison to Render Props and React Hooks:

[https://medium.com/simply/comparison-hocs-vs-render-props-vs-hooks-55f9ffcd5dc6](https://medium.com/simply/comparison-hocs-vs-render-props-vs-hooks-55f9ffcd5dc6)

### HOCs pitfalls

#### Don’t Use HOCs Inside the render Method

Apply HOCs outside the component definition so that the resulting component is created only once. Then, its identity will be consistent across renders. This is usually what you want, anyway.

Docs: [https://reactjs.org/docs/higher-order-components.html#dont-use-hocs-inside-the-render-method](https://reactjs.org/docs/higher-order-components.html#dont-use-hocs-inside-the-render-method)

#### Class Static Methods Must Be Copied Over

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

#### Refs Aren’t Passed Through

If you add a ref to an element whose component is the result of a HOC, the ref refers to an instance of the outermost container component, not the wrapped component.

How to solve: [<a href="https://reactjs.org/docs/higher-order-components.html#refs-arent-passed-through">https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)</a>

### Types of HOCs

* **Enhancers**: Wrap a component with additional functionality/props.
* **Injectors**: Inject props into a component.
* Recommended article about: [https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb](https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb)

## Render Props
### Example
```ts
interface InjectedCounterProps {
  value: number;
  onIncrement(): void;
  onDecrement(): void;
}

interface MakeCounterProps {
  minValue?: number;
  maxValue?: number;
  children(props: InjectedCounterProps): JSX.Element;
}

interface MakeCounterState {
  value: number;
}

class MakeCounter extends React.Component<MakeCounterProps, MakeCounterState> {
  state: MakeCounterState = {
    value: 0,
  };

  increment = () => {
    this.setState(prevState => ({
      value:
        prevState.value === this.props.maxValue
          ? prevState.value
          : prevState.value + 1,
    }));
  };

  decrement = () => {
    this.setState(prevState => ({
      value:
        prevState.value === this.props.minValue
          ? prevState.value
          : prevState.value - 1,
    }));
  };

  render() {
    return this.props.children({
      value: this.state.value,
      onIncrement: this.increment,
      onDecrement: this.decrement,
    });
  }
}
```
#### Usage
```ts
interface CounterProps {
  style: React.CSSProperties;
  minValue?: number;
  maxValue?: number;
}

const Counter = (props: CounterProps) => (
  <MakeCounter minValue={props.minValue} maxValue={props.maxValue}>
    {injectedProps => (
      <div style={props.style}>
        <button onClick={injectedProps.onDecrement}> - </button>
        {injectedProps.value}
        <button onClick={injectedProps.onIncrement}> + </button>
      </div>
    )}
  </MakeCounter>
);
```

### Issues of

* Firstly, there is an **issue with separation of concerns** with Render Props; if you wrap a component with a render prop in the same component, it will make it more difficult to test the two in isolation. May be fixed by creating more boilerplate code and creating separate component for what is rendered inside the render prop
* Secondly, as the props are injected in the render function of component, you cannot make use of them in the lifecycle methods
* Source: [https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c](https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c)

### Render Prop vs HOC

* In the end, the tradeoff between HOCs and render prop components comes down to **flexibility vs convenience**. This can be solved by writing render prop components first, then generating HOCs from them, which gives the consumer the power to choose between the two.
* As far as TypeScript goes, there is no doubt that typing HOCs is much more difficult.
* Prior to React v16.8.0, I’d recommend **sticking with render prop components for the flexibility and simplicity of typing**, and if the need arises, such as building a reusable library of components, or for render prop components that are simple and/or widely used across a project, I would only then generate a HOC from them.
* in React v16.8.0, I would strongly recommend using hooks over both higher-order components or render props where possible, as they are much simpler to type.
* Source: [https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c](https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c)

## React Hooks

### FAQ

* [Is there something like class instance variables so we won't need to use state and rerender component?](https://reactjs.org/docs/hooks-faq.html#is-there-something-like-instance-variables)
* `useEffect()` Hook is the equivalent of both the `componentDidMount()` and `componentDidUpdate()`

### Custom Hook versus HOC
```js
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
[source and comparison to standard HOC: https://dev.to/gethackteam/from-higher-order-components-hoc-to-react-hooks-2bm9](https://dev.to/gethackteam/from-higher-order-components-hoc-to-react-hooks-2bm9)

### Use only Hooks for global state management

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

