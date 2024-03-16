# static propTypes in React

In React, `static propTypes` is a class property that allows you to specify the expected types for props in a class component. It's used for type-checking props to ensure that they conform to the expected data types, improving code reliability and maintainability.

## Purpose

The primary purpose of `static propTypes` is to define the expected types for props in a component. By specifying propTypes, you can catch potential bugs caused by incorrect prop types early in development and provide clear documentation for component usage.

## Syntax

```jsx
import React from "react";
import PropTypes from "prop-types"; // Import PropTypes from the prop-types package

function MyComponent(props) {
  return <div>{props.name}</div>;
}

MyComponent.propTypes = {
  name: PropTypes.string.isRequired, // Specifies that the 'name' prop should be a string and is required
};

export default MyComponent;
```
