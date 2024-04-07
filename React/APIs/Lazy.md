# `Lazy`

`lazy` lets you defer loading component’s code until it is rendered for the first time.

```jsx
const SomeComponent = lazy(load);
```

Call `lazy` outside your components to declare a lazy-loaded React component:

## Params

`load`: A function that returns a Promise or another thenable (a Promise-like object with a `then` method).React will not call load until the first time you attempt to render the returned component.

## Return

`lazy` returns a React component you can render in your tree.

## Syntax

```jsx
import React, { Suspense, lazy } from "react";

// Define a component that will be lazily loaded
const LazyLoadedComponent = lazy(() => import("./LazyLoadedComponent"));

const App = () => {
  return (
    <div>
      <h1>Welcome to My App</h1>
      <Suspense fallback={<div>Loading...</div>}>
        {/* Render the lazily loaded component */}
        <LazyLoadedComponent />
      </Suspense>
    </div>
  );
};

export default App;
```
