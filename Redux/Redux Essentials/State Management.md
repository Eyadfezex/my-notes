# State Management

This React counter component demonstrates a self-contained app structure:

```jsx
function Counter() {
  // State: a counter value
  const [counter, setCounter] = useState(0);

  // Action: code that causes an update to the state when something happens
  const increment = () => {
    setCounter((prevCounter) => prevCounter + 1);
  };

  // View: the UI definition
  return (
    <div>
      Value: {counter} <button onClick={increment}>Increment</button>
    </div>
  );
}
```

- State: The source of truth driving the app.
- View: Declarative UI representation based on the current state.
- Actions: Events triggered by user input, updating the state.

It follows the "one-way data flow" principle:

- State defines the app's condition.
- UI reflects this state.
- Actions (e.g., button clicks) update the state.
- UI re-renders based on the updated state.

To handle shared state among components across the application, Redux provides a **centralized location outside the component tree.** This simplifies state management and ensures code predictability and maintainability by enforcing specific patterns for state updates.
