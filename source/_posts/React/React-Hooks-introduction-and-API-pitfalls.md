---
title: "React Hooks"
tags:
  - React
  - React Hooks
categories:
  - [React, Hooks]
date: 2019-12-01 10:00:00
---

* Hooks are **a new addition in React 16.8**. They let you use state and other React features without writing a class.
* Hooks allow you to reuse stateful logic without changing your component hierarchy.
* Without hooks mutually related code that changes together gets split apart different lifecycle methods. Hooks let you split one component into smaller functions based on what pieces are related (such as setting up a subscription or fetching data), rather than forcing a split based on lifecycle methods.

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

- if you call `useState` many times, you do it in the same order during every render
  - React relies on the order in which Hooks are called
  - React remembers initial order of calling hooks so we can't conditionally add or remove any new hook
- React will remember its current value between re-renders, and provide the most recent one to our function.
```js
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
```
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

- it serves the same purpose as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in React classes
- React will remember the function you passed (we’ll refer to it as our “effect”), and call it later after performing the DOM updates
- Hooks let you organize side effects in a component by what pieces are related (such as adding and removing a subscription), rather than forcing a split based on lifecycle methods
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
- the function passed to `useEffect` is going to be different on every render. This is intentional. In fact, this is what lets us read the count value from inside the effect without worrying about it getting stale. **Every time we re-render, we schedule a different effect, replacing the previous one**
- Unlike `componentDidMount` or `componentDidUpdate`, **effects scheduled with `useEffect` don’t block the browser from updating the screen**
#### Cleaning subscriptions
- we might want to set up a subscription to some external data source
- In a React class, you would typically set up a subscription in `componentDidMount`, and clean it up in `componentWillUnmount`
- that **function what we return from our effect is the optional cleanup mechanism for effects**
```js
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Specify how to clean up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```
- React performs the cleanup when the component unmounts. However, as we learned earlier, **effects run for every render and not just once**. This is why React **also cleans up effects from the previous render** before running the effects next time. We will discuss optimalization in next section.

#### Second parameter
- a second argument to `useEffect` that is the array of values that the effect depends on, so in below example the effect will be executed only when `props.source` changes:

```js
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    subscription.unsubscribe();
  };
}, [props.source]);
```
- this way you can tell React to **skip applying an effect if certain values haven’t changed between re-renders**
- this also works for effects that have a cleanup phase
- **If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array ([]) as a second argument**

### Hook `useContext`
* A component calling useContext will always re-render when the context value changes. If re-rendering the component is expensive, [you can optimize it by using memoization](https://github.com/facebook/react/issues/15156#issuecomment-474590693).


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

### Extracting custom hook
```js
import React, { useState, useEffect } from 'react';

function FriendListItem(props) {
  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```
to
```js
mport { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```
```js
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

## Sources

- [https://reactjs.org/docs/hooks-reference.html](https://reactjs.org/docs/hooks-reference.html)
- [https://hackernoon.com/why-react-hooks-a-developers-perspective-2aedb8511f38](https://hackernoon.com/why-react-hooks-a-developers-perspective-2aedb8511f38)
