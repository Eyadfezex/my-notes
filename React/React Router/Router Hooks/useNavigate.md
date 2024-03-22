# useNavigate

`useNavigate` is a React Router hook enabling **[programmatic](../Topics/Programmatically%20Navigate.md)** navigation between routes in a React application.

---

The `navigate` function has two **signatures**:

1- **Navigate to a specific route:** You can pass a string representing the route you want to navigate to, similar to how you would specify a `to` prop in a `Link` component.

2- **Navigate relative to the current location:** You can pass a number representing the delta you want to go in the history stack, similar to how you would use the `go` method on `history` object. A positive number means moving forward in the history, while a negative number means moving backward.

## Syntax

```jsx
import { useNavigate } from "react-router-dom";

function Register() {
  const navigate = useNavigate();

  // Navigate to a specific route
  const handleNavigateToDashboard = () => {
    // This will navigate to the '/dashboard' route
    navigate("/dashboard");
  };

  return (
    <div>
      <h1>Register</h1>
      <Form afterSubmit={handleNavigateToDashboard} />
    </div>
  );
}
```
