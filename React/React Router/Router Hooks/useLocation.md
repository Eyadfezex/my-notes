# `useLocation`

`useLocation` is a React Router hook that provides access to the current URL location in a React component.

## props

`location.state`:The state value of the location created by `<Link state>` or `navigate`.

### Syntax

```jsx
import React from "react";
import { useLocation } from "react-router-dom";

function MyComponent() {
  const location = useLocation();

  return (
    <div>
      <h1>Current Pathname: {location.pathname}</h1>
      <p>Search: {location.search}</p>
      <p>Hash: {location.hash}</p>
    </div>
  );
}

export default MyComponent;
```
