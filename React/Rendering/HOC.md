## HOC

A higher-order component (HOC) is an advanced technique in React for reusing component logic. HOCs are not part of the React API, per se. They are a pattern that emerges from React’s compositional nature.

Concretely, a higher-order component is a function that takes a component and returns a new component.

Whereas a component transforms props into UI, a higher-order component transforms a component into another component.

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
