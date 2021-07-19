---
title: Redux
tags:
  - React
  - Redux
  - React state management
categories:
  - [React, State management]
date: 2021-07-07
---
# Overview
* keeps the state of your app in a **single store**
* terms to learn: actions, reducers, action creators, dispatch, middleware, pure functions, immutability, selectors
* **reducer’s job is to return a new state**, even if that state is unchanged from the current one
* **do not mutate the state**. State is immutable

## Sample reducer
```js
function reducer(state = initialState, action) {
  switch(action.type) {
    case 'INCREMENT':
      return {
        count: state.count + 1
      };
    case 'DECREMENT':
      return {
        count: state.count - 1
      };
    default:
      return state;
  }
}
```


# Terms and methods
## `connect` method
* Using the `connect` function that comes with Redux, you can plug any component into Redux’s data store, and the component can pull out the data it requires.

### Example usage
```js
import React from 'react';
import { connect } from 'react-redux';

const Avatar = ({ user }) => (
  <img src={user.avatar}/>
);

const mapStateToProps = state => ({
  user: state.user
});

export { Avatar };
export default connect(mapStateToProps)(Avatar);
```

# Sources
* https://daveceddia.com/how-does-redux-work/