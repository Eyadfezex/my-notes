# useRef Hook

`useRef` is a Hook that lets you reference a value that’s not needed for rendering. [`for more info`](https://react.dev/reference/react/useRef)

```jsx
const ref = useRef(initialValue);
```

## Parameters

- `initialValue`: The value you want the ref object’s `current` property to be initially. It can be a value of any type. This argument is ignored after the initial render.

## Return

`useRef` returns an object with a single property:

- `current`: Initially, it's set to the `initialValue` you have passed. You can later set it to something else using `ref.current = newValue`. If you pass the ref object to React as a ref attribute to a JSX node, React will set its current property.

## Syntax

```jsx
import React, { useRef } from "react";

const MyComponent = () => {
  const inputRef = useRef(null);

  const handleClick = () => {
    // Focuses the input element when the button is clicked
    inputRef.current.focus();
  };

  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleClick}>Focus Input</button>
    </div>
  );
};

export default MyComponent;
```
