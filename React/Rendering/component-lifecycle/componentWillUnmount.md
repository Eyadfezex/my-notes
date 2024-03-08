## componentWillUnmount Lifecycle Method in React

In React, `componentWillUnmount` is a lifecycle method available in class components that is invoked immediately before a component is unmounted and removed from the DOM. It's used to perform cleanup tasks such as removing event listeners, canceling network requests, or unsubscribing from external data sources.

### Purpose

The primary purpose of `componentWillUnmount` is to perform cleanup actions that need to take place before a component is removed from the DOM. This ensures that resources associated with the component are properly cleaned up to prevent memory leaks or other issues.

### Syntax

```jsx
import React, { Component } from "react";

class MyComponent extends Component {
  constructor(props) {
    super(props);
    this.timerId = null;
  }

  componentDidMount() {
    // Start a timer when the component mounts
    this.timerId = setInterval(() => {
      console.log("Timer tick");
    }, 1000);
  }

  componentWillUnmount() {
    // Clean up the timer when the component is unmounted
    clearInterval(this.timerId);
    console.log("Component is unmounted, timer is cleared");
  }

  render() {
    return <div>My Component</div>;
  }
}

export default MyComponent;
```
