## useReducer Hook

`useReducer` is a React Hook that lets you add a [reducer](https://react.dev/learn/extracting-state-logic-into-a-reducer) to your component. [`for more info`](https://react.dev/reference/react/useReducer)

```jsx
const [state, dispatch] = useReducer(reducer, initialArg, init?)
```

## Parameters

- `reducer` :The reducer function that specifies how the state gets updated. It must be pure, should take the state and action as arguments, and should return the next state.

- `initialArg` :The value from which the initial state is calculated. It can be a value of any type.

- **optional** `init`: The initializer function that should return the initial state. If it’s not specified, the initial state is set to `initialArg`.

## Returns

`useReducer` returns an array with exactly two values:

- The current state. During the first render, it’s set to `init(initialArg)` or `initialArg` (if there’s no init).
- The dispatch function that lets you update the state to a different value and trigger a re-render.

## Syntax

```jsx
import React, { useReducer } from "react";

// Reducer function
const reducer = (state, action) => {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      return state;
  }
};

// Component using useReducer
const Counter = () => {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "INCREMENT" })}>Increment</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>Decrement</button>
    </div>
  );
};

export default Counter;
```
