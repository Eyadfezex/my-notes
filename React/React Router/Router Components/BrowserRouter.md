# Browser Router

`<BrowserRouter>`: provides a convenient and efficient way to implement client-side routing in React applications, allowing for seamless navigation and clean URL management.

## props

- `basename`:
  The basename prop in React Router lets you set a base URL for all routes in your app. It's handy when your app is hosted in a subdirectory, ensuring all route paths are relative to that subdirectory.

```jsx
function App() {
  return (
    <BrowserRouter basename="/app">
      <Routes>
        <Route path="/" /> {/* 👈 Renders at /app/ */}
      </Routes>
    </BrowserRouter>
  );
}
```

## Syntax

```jsx
import * as React from "react";
import { createRoot } from "react-dom/client";
import { BrowserRouter } from "react-router-dom";

const root = createRoot(document.getElementById("root"));

root.render(
  <BrowserRouter>{/* The rest of your app goes here */}</BrowserRouter>
);
```
