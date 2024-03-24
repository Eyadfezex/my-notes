# Navigate

The `<Navigate />` component in React Router enables programmatic redirection within a React application, ideal for scenarios like post-form submission or authentication.

## Props

`replace`: "replace" in `<Navigate>` swaps the current history entry with the new one. This means after login and redirection, users can't use the browser's back button to return to the protected page.

## Syntax

```jsx
import React from "react";
import { Navigate } from "react-router-dom";

function ExampleComponent({ isAuthenticated }) {
  // If user is authenticated, navigate to the dashboard
  if (isAuthenticated) {
    return <Navigate to="/dashboard" />;
  }
  // Otherwise, render the login form
  return <LoginForm />;
}

export default ExampleComponent;
```
