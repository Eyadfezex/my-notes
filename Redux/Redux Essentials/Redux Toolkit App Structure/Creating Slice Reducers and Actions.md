# Creating Slice Reducers and Actions

In the `features/counter/counterSlice.js` file, we define a Redux slice using the `createSlice` function from `@reduxjs/toolkit`. This slice manages the state for a counter feature.

Here's what's inside the file:

```javascript
import { createSlice } from "@reduxjs/toolkit";

export const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

This slice has:

- A name `'counter'` to identify it.
- An initial state with a `value` of 0.
- Three reducer functions: `increment`, `decrement`, and `incrementByAmount`, each modifying the state based on the dispatched action.

`createSlice` automatically generates action creators with the same names as the reducer functions. For instance, `counterSlice.actions.increment()` returns `{type: "counter/increment"}`.

It also generates the slice reducer function that knows how to respond to these action types. For example:

```javascript
const newState = counterSlice.reducer(
  { value: 10 },
  counterSlice.actions.increment()
);
console.log(newState); // {value: 11}
```

This demonstrates how Redux Toolkit simplifies the process of defining actions and reducers, reducing the need for manual action creation and enabling efficient state management.
