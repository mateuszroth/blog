---
title: React Hooks
tags:
  - React
  - React Hooks
categories:
  - [React, Hooks]
date: 2020-07-17 21:25:00
---
# React Hooks

## Methods

* basic hooks: `useState`, `useEffect`, `useContext`
* additional: `useReducer`, `useCallback`, `useMemo`, `useRef`, `useImperativeHandle`, `useLayoutEffect`, `useDebugValue`

### `setState`
* Unlike the `setState` method found in class components, `useState` does not automatically merge update objects.

```
setState(prevState => {
  // Object.assign would also work
  return {...prevState, ...updatedValues};
});
```
* Another option is `useReducer`, which is more suited for managing state objects that contain multiple sub-values.
* `setState` - If the initial state is the result of an expensive computation, you may provide a function instead, which will be executed only on the initial render

```
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

### `useEffect`
* you should call hooks at the top level of the render function, this means no conditional hooks
* a second argument to `useEffect` that is the array of values that the effect depends on:

```
useEffect(
  () => {
    const subscription = props.source.subscribe();
    return () => {
      subscription.unsubscribe();
    };
  },
  [props.source],
);
```

### `useMemo`
* If you’re doing expensive calculations while rendering, you can optimize them with `useMemo`.


## React Hooks advantages
* hooks are easier to test (as separated functions) and make the code look cleaner/easier to read (i.e. less LOCs)
* code that uses hooks is more readable and have less LOC (https://m.habr.com/en/post/443500/)
* hooks make code more reusable / composable (also they don't create another element in DOM like HOCs do)
* you can define several seperate lifecycle methods instead of having all in one method
* hooks are going to work better with future React optimizations (like ahead of time compilation and components folding) - components folding in future (https://github.com/facebook/react/issues/7323) - what means dead code elimination at compile time (less JS code to download, less to execute)
* hooks show real nature of React which is functional, using classes make developer easier to do mistakes and use React antipatterns
* hooks are very convenient to re-use stateful logic, this is one of their selling point. But this not applicable when app is built using some state management library and stateful logic doesn't live in React components. So for desktop in its current state hooks are mostly for readability and to make it future-proof.
* With HOCs we are separating unrelated state logic into different functions and injecting them into the main component as props, although with Hooks, we can solve this just like HOCs but without a wrapper hell (https://cdn-images-1.medium.com/max/2000/1*t4NuFEZWHcfPHV_f487GRA.png)


## React Hooks vs HOCs and render props
* https://www.freecodecamp.org/news/why-react-hooks-and-how-did-we-even-get-here-aa5ed5dc96af/
* https://cdn-images-1.medium.com/max/800/1*skhvS29DZ6sBkCPBmaMz7g.png
* mixins https://cdn-images-1.medium.com/max/800/1*nkp3K5sbw6FuGvoLofVk8g.png
* hocs https://cdn-images-1.medium.com/max/800/1*qJZXnzuAgXQsSoibXZH6Zg.png
* render props https://cdn-images-1.medium.com/max/800/1*ii7bRuk2u7jBqunmIzwGrQ.png
* hooks https://cdn-images-1.medium.com/max/800/1*11zyjavrNZlqDypso2EaeQ.png

## Function Components and Hooks in TypeScript example

```
// import useState next to FunctionComponent
import React, { FunctionComponent, useState } from 'react';

// our components props accept a number for the initial value
const Counter:FunctionComponent<{ initial?: number }> = ({ initial = 0 }) => {
  // since we pass a number here, clicks is going to be a number.
  // setClicks is a function that accepts either a number or a function returning
  // a number
  const [clicks, setClicks] = useState(initial);
  return <>
    <p>Clicks: {clicks}</p>
    <button onClick={() => setClicks(clicks+1)}>+</button>
    <button onClick={() => setClicks(clicks-1)}>-</button>
  </>
}
```

## Hooks with TypeScript
- Examples how to use with TS: https://fettblog.eu/typescript-react/hooks/
- TS advanced: https://medium.com/@jrwebdev/react-hooks-in-typescript-88fce7001d0d
- super advanced: https://levelup.gitconnected.com/usetypescript-a-complete-guide-to-react-hooks-and-typescript-db1858d1fb9c

```
const Counter:FunctionComponent<{ initial?: number }> = ({ initial = 0 }) => {
  ...
}
```

### with `useState`

```
// explicitly setting the types
const [value, setValue] = useState<number | undefined>(undefined);
const [value, setValue] = useState<Array<number>>([]);

interface MyObject {
  foo: string;
  bar?: number;
}
const [value, setValue] = useState<MyObject>({ foo: 'hello' });
```

### with `useRef`

```
const inputEl = useRef<HTMLInputElement>(null);
```

### with `useContext`

```
type Theme = 'light' | 'dark';
const ThemeContext = createContext<Theme>('dark');
```

### with `useReducer`

```
interface State {
  value: number;
}

type Action =
  | { type: 'increment' }
  | { type: 'decrement' }
  | { type: 'incrementAmount'; amount: number };

const counterReducer = (state: State, action: Action) => {
  switch (action.type) {
    case 'increment':
      return { value: state.value + 1 };
    case 'decrement':
      return { value: state.value - 1 };
    case 'incrementAmount':
      return { value: state.value + action.amount };
    default:
      throw new Error();
  }
};

const [state, dispatch] = useReducer(counterReducer, { value: 0 });

dispatch({ type: 'increment' });
dispatch({ type: 'decrement' });
dispatch({ type: 'incrementAmount', amount: 10 });

// TypeScript compilation error
dispatch({ type: 'invalidActionType' });
```