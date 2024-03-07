## static defaultProps in React

In React, `static defaultProps` is a class property that allows you to define default values for props in a class component. It's used to specify default values that will be used if the component is rendered without the corresponding prop being provided.

### Purpose

The primary purpose of `static defaultProps` is to provide fallback values for props in case they are not explicitly passed to the component. This helps to ensure that the component behaves as expected even if certain props are not provided by its parent components.

### Syntax

```jsx
import React, { Component } from "react";

class MyComponent extends Component {
  static defaultProps = {
    name: "Guest",
    age: 25,
  };

  render() {
    return (
      <div>
        <p>Name: {this.props.name}</p>
        <p>Age: {this.props.age}</p>
      </div>
    );
  }
}

export default MyComponent;
```
