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
