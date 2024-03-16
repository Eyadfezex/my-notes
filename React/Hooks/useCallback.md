# useCallback Hook

`useCallback` is a React Hook that lets you cache a function definition between re-renders.
[`For more info`](https://react.dev/reference/react/useCallback#)

```jsx
useCallback(fn, dependencies);
```

## Parameters

- `fn`: The function value that you want to cache.
- `dependencies`:he list of all reactive values referenced inside of the `fn` code.

## Returns

- On the initial render, useCallback returns the fn function you have passed.

## Syntax

```jsx
import React, { useState, useCallback } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  // Define a memoized increment function using useCallback
  const increment = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      {/* Use the memoized increment function */}
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```
