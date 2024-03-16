# useState Hook

- `useState` is a React Hook that lets you add a state variable to your component.
  [`For more info`](https://react.dev/reference/react/useState)

```jsx
const [state, setState] = useState(initialState);
```

## Parameters

- `initialState` : The value you want the state to be initially.

## Returns

- `useState` returns an array with exactly two values:

  - The current state. During the first render, it will match the initialState you have passed.
  - The set function that lets you update the state to a different value and trigger a re-render.

## Syntax

```jsx
import { useState } from 'react';

function MyComponent() {
  const [age, setAge] = useState(28);
  const [name, setName] = useState('Taylor');
  const [todos, setTodos] = useState(() => createTodos());
  // ...
```
