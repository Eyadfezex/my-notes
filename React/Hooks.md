Filtered notes on React Hooks:

- **Hooks** are a new addition in React 16.8. They let you use state and other React features without writing a class.

- **State hooks**:
  - A form component might have state to keep track of the current input value as the user types.
  - An image carousel component might use state to determine which image to display next.
  - A shopping cart component could use state to manage the list of items added by the user.

- To add state to a component, use one of these Hooks:
  - [`useState`](https://react.dev/reference/react/useState) declares a state variable that you can update directly.
  - [`useReducer`](https://react.dev/reference/react/useReducer) declares a state variable with the update logic inside a [reducer function.](https://react.dev/learn/extracting-state-logic-into-a-reducer)

- `useRef` is a React Hook that lets you reference a value that’s not needed for rendering.
  - Changing a ref does not trigger a re-render.
  - Do not write or read `ref.current` during rendering.

- `useCallback` is a React Hook that lets you cache a function definition between re-renders.

These notes provide a concise overview of the different React Hooks and their usage.
