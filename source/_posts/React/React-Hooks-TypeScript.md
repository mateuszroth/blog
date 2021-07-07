---
title: React Hooks with TypeScript
tags:
  - React
  - React Hooks
categories:
  - [React, Hooks]
date: 2020-07-17 21:25:00
---
## Function Components and Hooks in TypeScript example

```ts
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

```ts
const Counter:FunctionComponent<{ initial?: number }> = ({ initial = 0 }) => {
  ...
}
```

### with `useState`

```ts
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

```ts
const inputEl = useRef<HTMLInputElement>(null);
```

### with `useContext`

```ts
type Theme = 'light' | 'dark';
const ThemeContext = createContext<Theme>('dark');
```

### with `useReducer`

```ts
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