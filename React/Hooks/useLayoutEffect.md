## useLayoutEffect

`useLayoutEffect` is a version of [`useEffect`](./useEffect.md) that fires before the browser repaints the screen.

- `useEffect` runs after the browser has painted the screen, making it asynchronous.

- On the other hand, `useLayoutEffect` runs synchronously after all DOM mutations but before the browser has painted the screen.This makes it suitable for tasks that require immediate access to the DOM after an update, such as measuring elements or performing animations based on the current layout.

```jsx
useLayoutEffect(setup, dependencies?)
```

## Parameters

- `setup`:The function with your Effect’s logic. Your setup function may also optionally return a cleanup function.

- **optional** `dependencies`: The list of all reactive values referenced inside of the `setup` code. Reactive values include props, state, and all the variables and functions declared directly inside your component body.

## Syntax

```jsx
import React, { useState, useLayoutEffect } from "react";

function MyComponent() {
  const [width, setWidth] = useState(0);

  // This effect runs synchronously after DOM mutations
  useLayoutEffect(() => {
    // Measure the width of the element
    const newWidth = document.getElementById("myElement").clientWidth;
    // Update the state with the measured width
    setWidth(newWidth);
  }, []); // Empty dependency array means it only runs once after initial render

  return (
    <div>
      <div
        id="myElement"
        style={{ width: "200px", height: "100px", background: "red" }}
      >
        This is my element
      </div>
      <p>The width of the element is: {width}px</p>
    </div>
  );
}

export default MyComponent;
```
