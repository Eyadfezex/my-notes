# Hooks

- **Hooks** are a new addition in React 16.8. They let you use state and other React features without writing a class.

## Hooks rules

- All Hooks should called at the `top level` off component.
- Hooks don’t work inside classes.

## State hooks

- State lets a component “remember” information like user input. For example, a form component can use state to store the input value, while an image gallery component can use state to store the selected image index.

- To add state to a component, use one of these Hooks:

  - [`useState`](https://react.dev/reference/react/useState) declares a state variable that you can update directly.
  - [`useReducer`](https://react.dev/reference/react/useReducer) declares a state variable with the update logic inside a [reducer function.](https://react.dev/learn/extracting-state-logic-into-a-reducer)

## Context Hooks

- Context lets a component receive information from distant parents without passing it as props. For example, your app’s top-level component can pass the current UI theme to all components below, no matter how deep.

  - `useContext` reads and subscribes to a context.

## Ref Hooks

- Refs in React hold non-rendering information like DOM nodes or timeout IDs. They're an "escape hatch" from React's paradigm, useful for non-React systems like browser APIs.

- `useRef` declares a ref. You can hold any value in it, but most often it’s used to hold a DOM node.

- `useImperativeHandle` lets you customize the ref exposed by your component. This is rarely used.

## Effect Hooks

- Effects in React enable components to interact with external systems, such as network requests, browser DOM manipulation, animations, integration with different UI libraries' widgets, and other non-React code.

- `useEffect` connects a component to an external system.

## Performance Hooks

- To optimize re-rendering performance and skip unnecessary work in React, you can utilize hooks such as:

- `useMemo` lets you cache the result of an expensive calculation.
- `useCallback` lets you cache a function definition before passing it down to an optimized component.

## Resource Hooks

- Resources can be accessed by a component without having them as part of their state. For example, a component can read a message from a Promise or read styling information from a context.

- `use` lets you read the value of a resource like a Promise or context.
