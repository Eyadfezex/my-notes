## static getDerivedStateFromProps in React

In React, `static getDerivedStateFromProps` is a static lifecycle method available in class components that is invoked before rendering when new props are received. It allows the component to update its internal state based on changes in props, providing a way to synchronize the state with props.

### Purpose

The primary purpose of `static getDerivedStateFromProps` is to provide a way for a component to update its internal state based on changes in props. It's particularly useful when the component's state needs to be derived from its props, ensuring that the component stays in sync with external data.

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
    // Initialize state
  };

  render() {
    // Render JSX using state and props
  }
}
```
