## static getDerivedStateFromProps in React

In React, `static getDerivedStateFromProps` is a static lifecycle method available in class components that is invoked after new props are received but before the component is rendered. It allows the component to update its state based on changes in props.

### Purpose

The primary purpose of `static getDerivedStateFromProps` is to provide a mechanism for class components to update their internal state based on changes in props before rendering. It allows the component to synchronize its state with the incoming props.

## Parameters

- `props`: The next props that the component will receive.
- `state`: The current state of the component.

### Syntax

```jsx
class MyComponent extends React.Component {
  static getDerivedStateFromProps(props, state) {
    // Return an object to update state based on props
  }

  state = {
    // Initial state
  };

  render() {
    // Render JSX using state and props
  }
}
```
