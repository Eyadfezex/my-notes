# `<Suspense>`

`<Suspense>` lets you display a fallback until its children have finished loading.

```jsx
<Suspense fallback={<Loading />}>
  <SomeComponent />
</Suspense>
```

## props

`children`: actual UI you intend to render. If `children` suspends while rendering, the Suspense boundary will switch to rendering `fallback`.

`fallback`:An alternate UI to render in place of the actual UI if it has not finished loading.

## Syntax

```jsx
import React, { Suspense } from "react";

// Lazy-loaded component
const LazyComponent = React.lazy(() => import("./LazyComponent"));

const App = () => {
  return (
    <div>
      <h1>Welcome to My App</h1>
      <Suspense fallback={<div>Loading...</div>}>
        {/* Lazy-loaded component wrapped in Suspense */}
        <LazyComponent />
      </Suspense>
    </div>
  );
};

export default App;
```
