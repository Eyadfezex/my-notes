# Nested Routes

Nested routes in React Router involve organizing routes within other routes, creating a hierarchical structure for rendering components based on URL segments.
![alt text](../../img//nestedRoutes.png)

- Component Definition: Home, about, contact, and product pages are defined.

- Nested Routes: Routes for product categories like electronics and clothing are configured within the products page.

- Navigation Menu: A navigation menu enables easy movement between app sections.

- Enhanced Code Organization: The code is structured to simplify managing routing complexities.

## Example

```jsx
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";

const App = () => {
  return (
    <Router>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
        <Route path="/products" component={Products}>
          <Route path="/products/electronics" component={Electronics} />
          <Route path="/products/clothing" component={Clothing} />
        </Route>
      </Switch>
    </Router>
  );
};
```
