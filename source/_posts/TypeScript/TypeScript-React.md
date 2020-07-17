---
title: TypeScript with React
tags:
  - React
  - React Hooks
  - TypeScript
categories:
  - [React, Hooks]
  - [React, TypeScript]
date: 2019-12-01 16:13:00
---

# Common Operators and Signatures

### Type intersection operator (&)

```js
class WithLoading extends React.Component<P & WithLoadingProps> { ... }
```

### Generic function

```js
const funcComponent = <P extends object>(Component: React.ComponentType<P>): ... => { ... }
```

### Type cast

A type cast (props as P) is required when passing props forward from TypeScript v3.2 onwards, due to a likely bug in TypeScript.

```js
return loading ? <LoadingSpinner /> : <Component {...props as P} />;
```

# Examples

Worth to read:

- about HOCs: [https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb](https://medium.com/@jrwebdev/react-higher-order-component-patterns-in-typescript-42278f7590fb)

## Higher Order Components

### Higher Order Component in JS

```js
const withLoading = Component =>
  class WithLoading extends React.Component {
    render() {
      const { loading, ...props } = this.props;
      return loading ? <LoadingSpinner /> : <Component {...props} />;
    }
  };
```

### Higher Order Component in TS

```ts
interface WithLoadingProps {
  loading: boolean;
}

const withLoading = <P extends object>(Component: React.ComponentType<P>) =>
  class WithLoading extends React.Component<P & WithLoadingProps> {
    render() {
      const { loading, ...props } = this.props;
      return loading ? <LoadingSpinner /> : <Component {...props as P} />;
    }
  };
```

### Function Higher Order Component in TS

```ts
const withLoading = <P extends object>(
  Component: React.ComponentType<P>
): React.FC<P & WithLoadingProps> => ({
  loading,
  ...props
}: WithLoadingProps) =>
  loading ? <LoadingSpinner /> : <Component {...props as P} />;
```

### Render Prop Component

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
[make-counter-render-prop.tsx](https://gist.github.com/jrwebdev/b8fea9723d4f86743c29a1888dbbe090#file-make-counter-render-prop-tsx)

### Usage

```tsx
interface CounterProps extends InjectedCounterProps {
  style: React.CSSProperties;
}

const Counter = (props: CounterProps) => (
  <div style={props.style}>
    <button onClick={props.onDecrement}> - </button>
    {props.value}
    <button onClick={props.onIncrement}> + </button>
  </div>
);

interface WrappedCounterProps extends CounterProps {
  minValue?: number;
  maxValue?: number;
}

const WrappedCounter = ({
  minValue,
  maxValue,
  ...props
}: WrappedCounterProps) => (
  <MakeCounter minValue={minValue} maxValue={maxValue}>
    {injectedProps => <Counter {...props} {...injectedProps} />}
  </MakeCounter>
);
```
[wrapped-counter.tsx](https://gist.github.com/jrwebdev/c0392dfc25d3fc30893f324a89c8a16d#file-wrapped-counter-tsx)

### Wrapping Render Prop as HOC

```ts
import { Subtract, Omit } from 'utility-types';
import MakeCounter, { MakeCounterProps, InjectedCounterProps } from './MakeCounter';

type MakeCounterHocProps = Omit<MakeCounterProps, 'children'>;

const makeCounter = <P extends InjectedCounterProps>(
  Component: React.ComponentType<P>
): React.SFC<Subtract<P, InjectedCounterProps> & MakeCounterHocProps> => ({
  minValue,
  maxValue,
  ...props
}: MakeCounterHocProps) => (
  <MakeCounter minValue={minValue} maxValue={maxValue}>
    {injectedProps => <Component {...props as P} {...injectedProps} />}
  </MakeCounter>
);
```

Source: [https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c](https://medium.com/@jrwebdev/react-render-props-in-typescript-b561b00bc67c)

## React Hooks

### Function Components with Hooks in TS example

```ts
// import useState next to FunctionComponent
import React, { FunctionComponent, useState } from "react";

// our components props accept a number for the initial value
const Counter: FunctionComponent<{ initial?: number }> = ({ initial = 0 }) => {
  // since we pass a number here, clicks is going to be a number.
  // setClicks is a function that accepts either a number or a function returning
  // a number
  const [clicks, setClicks] = useState(initial);
  return (
    <>
      <p>Clicks: {clicks}</p>
      <button onClick={() => setClicks(clicks + 1)}>+</button>
      <button onClick={() => setClicks(clicks - 1)}>-</button>
    </>
  );
};
```

# Details about React Hooks with TypeScript

- Examples how to use with TS: [https://fettblog.eu/typescript-react/hooks/](https://fettblog.eu/typescript-react/hooks/)
- TS advanced: [https://medium.com/@jrwebdev/react-hooks-in-typescript-88fce7001d0d](https://medium.com/@jrwebdev/react-hooks-in-typescript-88fce7001d0d)
- super advanced: [https://levelup.gitconnected.com/usetypescript-a-complete-guide-to-react-hooks-and-typescript-db1858d1fb9c](https://levelup.gitconnected.com/usetypescript-a-complete-guide-to-react-hooks-and-typescript-db1858d1fb9c)

```ts
const Counter:FunctionComponent<{ initial?: number }> = ({ initial = 0 }) => {
  ...
}
```

### with `useState`

```ts
// explicitly setting the types
const [value, setValue] = (useState < number) | (undefined > undefined);
const [value, setValue] = useState < Array < number >> [];

interface MyObject {
  foo: string;
  bar?: number;
}
const [value, setValue] = useState <MyObject> { foo: "hello" };
```

### with `useRef`

```ts
const inputEl = useRef <HTMLInputElement> null;
```

### with `useContext`

```ts
type Theme = "light" | "dark";
const ThemeContext = createContext <Theme> "dark";
```

### with `useReducer`

```ts
interface State {
  value: number;
}

type Action =
  | { type: "increment" }
  | { type: "decrement" }
  | { type: "incrementAmount", amount: number };

const counterReducer = (state: State, action: Action) => {
  switch (action.type) {
    case "increment":
      return { value: state.value + 1 };
    case "decrement":
      return { value: state.value - 1 };
    case "incrementAmount":
      return { value: state.value + action.amount };
    default:
      throw new Error();
  }
};

const [state, dispatch] = useReducer(counterReducer, { value: 0 });

dispatch({ type: "increment" });
dispatch({ type: "decrement" });
dispatch({ type: "incrementAmount", amount: 10 });

// TypeScript compilation error
dispatch({ type: "invalidActionType" });
```
