## componentDidCatch Lifecycle Method in React

In React, `componentDidCatch` is a lifecycle method available in class components that is invoked when an error occurs within the component tree of a class component. It provides a way to catch and handle errors that occur during rendering, in lifecycle methods, or in the constructor of any child component.

### Purpose

The primary purpose of `componentDidCatch` is error handling and error boundary creation. An error boundary is a React component that catches JavaScript errors anywhere in its child component tree, logs those errors, and displays a fallback UI instead of crashing the entire component tree.

## Parameters

- `error`: The error that was thrown.
- `info`: An object containing information about the error, including its component stack trace.

### Syntax

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  componentDidCatch(error, errorInfo) {
    // Update state to display fallback UI
    this.setState({ hasError: true });
    // Log error details
    console.error("Error caught by ErrorBoundary:", error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // Fallback UI
      return <h1>Something went wrong.</h1>;
    }

    // Render children normally
    return this.props.children;
  }
}
```
