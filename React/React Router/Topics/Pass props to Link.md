# Passing Props to Components in React Router

In React Router, routes map URLs to specific components in your application. These components often need additional data, such as user information, product IDs, or specific views to display. This guide demonstrates how to pass props to components within a route and how to create links to dynamic items.

## Defining Routes and Passing Props

You can directly define the component element to render within a route and pass props just like any other React component.

### Example: Passing Props to a Route Component

```jsx
import React from "react";
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import ProductDetails from "./ProductDetails";

function App() {
  return (
    <Router>
      <Routes>
        <Route
          path="/products/:productId"
          element={<ProductDetails someProp="someValue" />}
        />
      </Routes>
    </Router>
  );
}

export default App;
```

In this example, `someProp` is passed to the `ProductDetails` component.

## Using `useParams` to Access URL Parameters

To get the prop from the URL, use the `useParams` hook from `react-router-dom`.

### Example: Accessing URL Parameters

```jsx
import React from "react";
import { useParams } from "react-router-dom";

function ProductDetails({ someProp }) {
  const { productId } = useParams();

  return (
    <div>
      <h1>Product ID: {productId}</h1>
      <p>Prop passed from route: {someProp}</p>
    </div>
  );
}

export default ProductDetails;
```

## Creating Links to Dynamic Items

You can create links to dynamic items using the `Link` component from `react-router-dom`.

### Example: Linking to Dynamic Items

```jsx
import React from "react";
import { Link } from "react-router-dom";
import { getPosts } from "./api";

function Home() {
  const posts = getPosts();

  return (
    <div>
      <h1>Posts</h1>
      <nav>
        <ul>
          {posts.map(({ id, title }) => (
            <li key={id}>
              <Link to={`/blog/${id}`}>{title}</Link>
            </li>
          ))}
        </ul>
      </nav>
    </div>
  );
}

export default Home;
```

### Full Example

Combining all the pieces, here's a complete example:

```jsx
import React from "react";
import {
  BrowserRouter as Router,
  Route,
  Routes,
  Link,
  useParams,
} from "react-router-dom";

// Dummy function to simulate fetching posts
function getPosts() {
  return [
    { id: 1, title: "Post 1" },
    { id: 2, title: "Post 2" },
  ];
}

function Home() {
  const posts = getPosts();

  return (
    <div>
      <h1>Posts</h1>
      <nav>
        <ul>
          {posts.map(({ id, title }) => (
            <li key={id}>
              <Link to={`/blog/${id}`}>{title}</Link>
            </li>
          ))}
        </ul>
      </nav>
    </div>
  );
}

function PostDetails() {
  const { id } = useParams();

  return (
    <div>
      <h1>Post ID: {id}</h1>
    </div>
  );
}

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/blog/:id" element={<PostDetails />} />
      </Routes>
    </Router>
  );
}

export default App;
```

In this example:

- `Home` component displays a list of posts with links to individual post details.
- `PostDetails` component uses `useParams` to access the `id` parameter from the URL.
- `App` component sets up the routes using `react-router-dom`.
