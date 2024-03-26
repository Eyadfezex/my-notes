# Reducers

A reducer is a function that receives the current `state` and an [`action`](./Actions.md) object, decides how to update the state if necessary, and returns the new state: `(state, action) => newState`.

Reducers must adhere to specific rules:

1. Calculate the new state based on the state and action arguments.
2. Make immutable updates by copying the existing state and modifying the copied values.
3. Avoid asynchronous logic, random value calculation, or side effects.

The logic inside reducer functions typically involves:

1. Checking if the reducer handles the action.
2. Making a copy of the state, updating it with new values, and returning the copy if applicable.
3. Otherwise, returning the existing state unchanged.

Here's an example of a reducer following these steps:

```js
const initialState = { value: 0 };

function counterReducer(state = initialState, action) {
  // Check to see if the reducer cares about this action
  if (action.type === "counter/increment") {
    // If so, make a copy of `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1,
    };
  }
  // otherwise return the existing state unchanged
  return state;
}
```

Reducers can employ various logic methods, such as if/else, switch, or loops, to determine the new state.
