## HOC

A Higher-Order Component is a pattern in React where a function takes a component and returns a new component with added functionality. It's a way of enhancing or modifying existing components in a composable manner.

## Use Cases :

- Code Reusability: HOCs promote reusability by encapsulating common functionalities that can be applied to multiple components.

- Cross-cutting Concerns: HOCs are often used for concerns that span multiple components, such as logging, authentication, or route handling.

- Props Injection: HOCs can inject additional props or behavior into components without modifying the components themselves.

- Conditional Rendering: HOCs can conditionally render components based on certain conditions.

## Syntax

```jsx
import React from "react";

// Higher-order component function
const withLogging = (WrappedComponent) => {
  // Return a new component
  return class extends React.Component {
    componentDidMount() {
      console.log("Component is mounted");
    }

    render() {
      // Render the wrapped component with its props
      return <WrappedComponent {...this.props} />;
    }
  };
};

// Usage: Wrap a component with the higher-order component
const MyComponentWithLogging = withLogging(MyComponent);
```
