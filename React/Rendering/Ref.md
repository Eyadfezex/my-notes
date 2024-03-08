## Ref

When you want a component to “remember” some information,
but you don’t want that information to trigger new renders, you can use a ref.

## Differences between refs and state

|                | `useRef(initialValue)`                                            | `useState(initialValue)`                                                                                  |
| -------------- | ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Returns**    | `{ current: initialValue }`                                       | `[value, setValue]`                                                                                       |
| **Re-render**  | Doesn’t trigger re-render when you change it.                     | Triggers re-render when you change it.                                                                    |
| **Mutability** | Mutable—you can modify and update `current`'s value.              | "Immutable"—you must use the state setting function to modify state variables.                            |
| **Reading**    | You shouldn’t read (or write) the current value during rendering. | You can read state at any time. However, each render has its own snapshot of state which does not change. |

## Purpose

Refs are commonly used in React when components need to interact with external APIs, such as browser APIs, without affecting the component's appearance. Typical scenarios include:

- Storing timeout IDs.
- Managing DOM elements (covered next).
- Storing other non-JSX calculation related objects.

```jsx
import React, { useRef, useEffect } from "react";

const TextInput = () => {
  const inputRef = useRef(null);

  useEffect(() => {
    // Focus the input element when the component mounts
    inputRef.current.focus();
  }, []);

  return (
    <div>
      {/* Assign ref to the input element */}
      <input type="text" ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus Input</button>
    </div>
  );
};

export default TextInput;
```
