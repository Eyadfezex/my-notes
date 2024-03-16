# useDebugValue Hook

`useDebugValue` is a React Hook that lets you add a label to a custom Hook in [React DevTools](https://react.dev/learn/react-developer-tools).

```jsx
useDebugValue(value, format?)
```

## Parameters

- `value`: The value you want to display in React DevTools. It can have any type.

- **optional** `format`: A formatting function. When the component is inspected, React DevTools will call the formatting function with the `value` as the argument, and then display the returned formatted value (which may have any type).

## Syntax

```jsx
import React, { useState, useDebugValue } from "react";

function useCustomHook(initialValue) {
  const [value, setValue] = useState(initialValue);

  // This will display 'Custom Hook Value: <value>' in React DevTools
  useDebugValue(value, () => `Custom Hook Value: ${value}`);

  return [value, setValue];
}

function Component() {
  const [value, setValue] = useCustomHook(0);

  return (
    <div>
      <p>Value: {value}</p>
      <button onClick={() => setValue(value + 1)}>Increment</button>
    </div>
  );
}

export default Component;
```
