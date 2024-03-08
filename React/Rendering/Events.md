## Events

React lets you add event handlers to your JSX. Event handlers are your own functions that will be triggered in response to interactions like clicking, hovering, focusing form inputs, and so on.

### Purpose

React events enable components to respond to user interactions and system changes efficiently, ensuring a smooth and interactive user experience within a component-based architecture.

### Syntax

```jsx
import React from "react";

const MyComponent = () => {
  // Event handler function
  const handleClick = () => {
    console.log("Button clicked");
  };

  return (
    <div>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
};

export default MyComponent;
```
