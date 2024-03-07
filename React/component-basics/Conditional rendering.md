## Conditional Rendering in React

Conditional rendering in React allows you to display different components or UI elements based on conditions or state values. This flexibility enables you to dynamically control what appears on the screen, depending on user interactions or application logic.

### Methods for Conditional Rendering

1. **JavaScript Conditional Statements**:

   - You can use traditional JavaScript `if`, `else if`, and `else` statements to conditionally render components or elements based on certain conditions.

2. **Ternary Operators**:

   - Ternary operators (`condition ? true : false`) are often used for inline conditional rendering in JSX. They allow you to render different components or elements based on a condition.

3. **Logical AND (`&&`) Operator**:

   - The logical AND (`&&`) operator is commonly used for conditional rendering when you want to render a component or element only if a certain condition is true.

4. **Conditional Rendering Outside JSX**:
   - Conditional rendering can also be performed outside JSX, by conditionally rendering components or elements in JavaScript code before returning JSX in the `render()` method.

### Example

```jsx
import React, { useState } from "react";

function ExampleComponent() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <div>
      {isLoggedIn ? (
        <h1>Welcome, User!</h1>
      ) : (
        <button onClick={() => setIsLoggedIn(true)}>Login</button>
      )}
    </div>
  );
}
```
