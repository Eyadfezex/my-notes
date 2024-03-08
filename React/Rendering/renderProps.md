## Render Props

In React, a common pattern is to use render props. This pattern allows you to pass a component as a prop to another component and have that parent component control the child component

### Purpose

The purpose of using render props in React is to allow components to share code by passing a function as a prop. This enables greater reusability, customization, and flexibility in rendering logic, promoting cleaner and more modular component design.

### Syntax

```jsx
// ParentComponent.js
import React from 'react';
import ChildComponent from './ChildComponent';

const ParentComponent = () => {
  return (
    <div>
      {/* Pass a render prop to ChildComponent */}
      <ChildComponent render={(data) => (
        <div>
          <h1>{data.title}</h1>
          <p>{data.content}</p>
        </div>
      )} />
    </div>
  );
}

export default ParentComponent;

// ChildComponent.js
import React from 'react';

const ChildComponent = ({ render }) => {
  const state = {
    title: 'Render Props Example',
    content: 'This is a simple example of using render props in React.'
  };

  // Call the render prop function passed by the parent
  return render(state);
}

export default ChildComponent;

```
