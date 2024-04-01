# `useSelector`

The `useSelector` hook from React Redux bridges the gap between React components and the Redux store. It allows components to grab specific state slices they need, promoting cleaner and more performant code.

**How it Works:**

- Import `useSelector` from `react-redux`.
- Within your component, use `useSelector` with a selector function.
- The selector function receives the entire state and returns the desired slice.

**Benefits:**

- Targeted state access for components.
- Improved code readability and maintainability.
- Optimized performance with built-in memoization.

**Example:**

```javascript
import React from "react";
import { useSelector } from "react-redux";

const MyComponent = () => {
  const counter = useSelector((state) => state.counter);
  const userName = useSelector((state) => state.user.name);

  return (
    <div>
      <p>Counter: {counter}</p>
      <p>User: {userName}</p>
    </div>
  );
};
```

`useSelector` is a powerful tool for building well-connected and efficient Redux applications.
