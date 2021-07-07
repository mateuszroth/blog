---
title: "React Hooks"
tags:
  - React
  - React Hooks
categories:
  - [React, Hooks]
date: 2019-12-01 10:00:00
---

- Hooks are **a new addition in React 16.8**. They let you use state and other React features without writing a class.

## React Hooks advantages
* hooks are **easier to test** (as separated functions) and make the code look cleaner/easier to read (i.e. less LOCs)
* code that uses hooks is **more readable** and have less LOC (https://m.habr.com/en/post/443500/)
* hooks **make code more reusable / composable** (also they don't create another element in DOM like HOCs do)
* you can **define several seperate lifecycle methods instead of having all in one method**
* hooks are going to work better with **future React optimizations** (like ahead of time compilation and components folding) - components folding in future (https://github.com/facebook/react/issues/7323) - what means **dead code elimination at compile time** (less JS code to download, less to execute)
* hooks show real nature of React which is **functional, using classes make developer easier to do mistakes and use React antipatterns**
* hooks are very convenient to re-use stateful logic, this is one of their selling point. But this not applicable when app is built using some state management library and stateful logic doesn't live in React components. So for desktop in its current state hooks are mostly for readability and to make it future-proof.
* With HOCs we are separating unrelated state logic into different functions and injecting them into the main component as props, although with Hooks, we can solve this just like HOCs but without a wrapper hell (https://cdn-images-1.medium.com/max/2000/1*t4NuFEZWHcfPHV_f487GRA.png)


## React Hooks vs HOCs and render props
* https://www.freecodecamp.org/news/why-react-hooks-and-how-did-we-even-get-here-aa5ed5dc96af/
* https://cdn-images-1.medium.com/max/800/1*skhvS29DZ6sBkCPBmaMz7g.png
* mixins https://cdn-images-1.medium.com/max/800/1*nkp3K5sbw6FuGvoLofVk8g.png
* hocs https://cdn-images-1.medium.com/max/800/1*qJZXnzuAgXQsSoibXZH6Zg.png
* render props https://cdn-images-1.medium.com/max/800/1*ii7bRuk2u7jBqunmIzwGrQ.png
* hooks https://cdn-images-1.medium.com/max/800/1*11zyjavrNZlqDypso2EaeQ.png

## Hooks list

- basic hooks: `useState`, `useEffect`, `useContext`
- additional hooks: `useReducer`, `useCallback`, `useMemo`, `useRef`, `useImperativeHandle`, `useLayoutEffect`, `useDebugValue`

### Hook `setState`

- unlike the `setState` method found in class components, `useState` does not automatically merge update objects, so we have to manually set state for previous state values that we're not intend to modify:

```js
setState(prevState => {
  // Object.assign would also work
  return { ...prevState, ...updatedValues };
});
```

- alternative to the `setState` hook is the `useReducer` hook, which is more suited for managing state objects that contain multiple sub-values and not simple primitives like numbers, strings.
- `setState` - if the initial state is the result of an expensive computation, you may provide a function instead, which will be executed only on the initial render:

```js
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```

### Hook `useEffect`

- you should call hooks at the top level of the render function, this means no conditional hooks:

```js
// BAD:
if (user.isAdmin) {
  useEffect(() => {
    ...
  });
};

// GOOD:
useEffect(() => {
  if (user.isAdmin) {
    ...
  };
})
```

- a second argument to `useEffect` that is the array of values that the effect depends on, so in below example the effect will be executed only when `props.source` changes:

```js
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    subscription.unsubscribe();
  };
}, [props.source]);
```

### Hook `useCallback`

- returns a [memoized](https://en.wikipedia.org/wiki/Memoization) callback
- will return a memoized version of the callback that only changes if one of the dependencies has changed

```js
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

### Hook `useMemo`

- If you’re doing expensive calculations while rendering, you can optimize them with `useMemo`:

```js
const [c1, setC1] = useState(0);
const [c2, setC2] = useState(0);

// This value will not be recomputed between re-renders
// unless the value of c1 changes
const sinOfC1: number = useMemo(() => Math.sin(c1), [c1]);
```

- `useMemo` is generalized version of  `useCallback` hook. `useMemo` is primarily used for caching values but can also be used for caching functions as `useCallback` is used for because `useCallback(fn, deps)` is equivalent to `useMemo(() => fn, deps)`:

```js
// Some function ...
const f = () => { ... }

// The following are functionally equivalent
const callbackF = useCallback(f, [])
const callbackF = useMemo(() => f, [])
```

## Sources

- [https://reactjs.org/docs/hooks-reference.html](https://reactjs.org/docs/hooks-reference.html)
- [https://hackernoon.com/why-react-hooks-a-developers-perspective-2aedb8511f38](https://hackernoon.com/why-react-hooks-a-developers-perspective-2aedb8511f38)
