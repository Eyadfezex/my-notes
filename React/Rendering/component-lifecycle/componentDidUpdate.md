# componentDidUpdate Lifecycle Method in React

In React, `componentDidUpdate` is a lifecycle method available in class components that is invoked immediately after updating occurs. It's called after a component's state or props have been updated, but before the component re-renders.

## Purpose

The primary purpose of `componentDidUpdate` is to perform actions that need to take place after the component's state or props have been updated and the component has re-rendered. This includes tasks such as:

- Performing side effects based on changes in props or state.
- Updating the DOM in response to state changes.
- Fetching additional data when props change.

## Parameters

- `prevProps`: The previous props before the update.
- `prevState`: The previous state before the update.
- `snapshot`: An optional value returned by the `getSnapshotBeforeUpdate()` method.

## Syntax

```jsx
import React, { Component } from "react";

class MyComponent extends Component {
  componentDidUpdate(prevProps, prevState) {
    // Check if the prop 'data' has changed
    if (prevProps.data !== this.props.data) {
      // Perform some action based on the updated data
      console.log("Data has changed:", this.props.data);
    }
  }

  render() {
    return <div>{this.props.data}</div>;
  }
}

export default MyComponent;
```
