# Code Splitting with React & React Router

To handle code splitting with React Router, chunks of your application's code are loaded asynchronously when required, reducing the initial bundle size and optimizing performance.

React's [`Suspense`](../../components/Suspense.md) component can be used to specify a fallback element to display while the component loads, minimizing the waiting time for users before the UI is rendered.

[`React.lazy`](../../APIs/Lazy.md), along with dynamic imports, aids in code splitting. It accepts a function invoking a dynamic import as its argument and returns a standard React Component.

## Example

```jsx
import React, { Suspense } from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

// Use React.lazy to dynamically import components
const Home = React.lazy(() => import("./components/Home"));
const About = React.lazy(() => import("./components/About"));
const Contact = React.lazy(() => import("./components/Contact"));

// Loading component to show while components are being loaded
const Loading = () => <div>Loading...</div>;

const App = () => {
  return (
    <Router>
      <Suspense fallback={<Loading />}>
        <Switch>
          {/* Route for Home component */}
          <Route exact path="/" component={Home} />

          {/* Route for About component */}
          <Route path="/about" component={About} />

          {/* Route for Contact component */}
          <Route path="/contact" component={Contact} />
        </Switch>
      </Suspense>
    </Router>
  );
};

export default App;
```
