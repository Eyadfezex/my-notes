## componentWillUnmount Lifecycle Method in React

In React, `componentWillUnmount` is a lifecycle method available in class components that is invoked immediately before a component is unmounted and removed from the DOM. It's used to perform cleanup tasks such as removing event listeners, canceling network requests, or unsubscribing from external data sources.

### Purpose

The primary purpose of `componentWillUnmount` is to perform cleanup actions that need to take place before a component is removed from the DOM. This ensures that resources associated with the component are properly cleaned up to prevent memory leaks or other issues.

### Syntax

```jsx
class MyComponent extends React.Component {
  componentWillUnmount() {
    // Perform cleanup tasks, unsubscribe, remove event listeners, etc.
  }

  render() {
    // Render JSX
  }
}
```
