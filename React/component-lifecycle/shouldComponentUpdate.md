## shouldComponentUpdate Lifecycle Method in React

In React, `shouldComponentUpdate` is a lifecycle method available in class components that is invoked before rendering when new props or state are being received. It allows the component to control whether or not the component should re-render based on the changes in props or state.

### Purpose

> The primary purpose of `shouldComponentUpdate` is to optimize performance by preventing unnecessary re-renders of a component. By implementing this > method, a component can compare incoming props or state with the current props or state and decide whether a re-render is necessary.

## Parameters

- `nextProps`: The next props that the component will receive.
- `nextState`: The next state that the component will have.
- `nextContext`: The next context that the component will receive, if using context API.

## Return Value

- It's return `true` by default (`true`=re-render , `false`=Do note re-render)

### Syntax

```jsx
class MyComponent extends React.Component {
  shouldComponentUpdate(nextProps, nextState) {
    // Return true if the component should re-render
    // Return false if the component should not re-render
  }

  render() {
    // Render JSX
  }
}
```
