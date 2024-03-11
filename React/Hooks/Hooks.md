## Hooks

- **Hooks** are a new addition in React 16.8. They let you use state and other React features without writing a class.

## State hooks:

- A form component might have state to keep track of the current input value as the user types.
- An image carousel component might use state to determine which image to display next.
- A shopping cart component could use state to manage the list of items added by the user.

- To add state to a component, use one of these Hooks:

  - [`useState`](https://react.dev/reference/react/useState) declares a state variable that you can update directly.
  - [`useReducer`](https://react.dev/reference/react/useReducer) declares a state variable with the update logic inside a [reducer function.](https://react.dev/learn/extracting-state-logic-into-a-reducer)

## Context Hooks

- Context lets a component receive information from distant parents without passing it as props. For example, your app’s top-level component can pass the current UI theme to all components below, no matter how deep.

  - `useContext` reads and subscribes to a context.

```jsx
function Button() {
  const theme = useContext(ThemeContext);
  // ...
```

## Ref Hooks

- Refs in React hold non-rendering information like DOM nodes or timeout IDs. They're an "escape hatch" from React's paradigm, useful for non-React systems like browser APIs.

- `useRef` declares a ref. You can hold any value in it, but most often it’s used to hold a DOM node.

- `useImperativeHandle` lets you customize the ref exposed by your component. This is rarely used.

```jsx
function Form() {
  const inputRef = useRef(null);
  // ...

```

## Effect Hooks

- Effects let a component connect to and synchronize with external systems. This includes dealing with network, browser DOM, animations, widgets written using a different UI library, and other non-React code.

- `useEffect` connects a component to an external system.

```jsx
function ChatRoom({ roomId }) {
  useEffect(() => {
    const connection = createConnection(roomId);
    connection.connect();
    return () => connection.disconnect();
  }, [roomId]);
  // ...
```
