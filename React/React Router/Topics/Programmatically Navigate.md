# Programmatically Navigate

Using React Router API to control navigation within a React application, allowing for seamless transitions between different routes or pages based on logic defined in the code.

There are two ways to programmatically navigate with React Router - [`<Navigate />`](../Router%20Components/Navigate.md) and [`useNavigate().`](../Router%20Hooks/useNavigate.md)

---

## Declarative Navigation with `<Navigate />`

Using React Router, [`<Navigate />`](../Router%20Components/Navigate.md) component is a key tool for programmatically navigating. Despite its unconventional approach, it proves effective. For instance, we can use it to direct users to the /dashboard route upon completing registration.

example:

```jsx
import { Navigate } from "react-router-dom";

function Register() {
  const [toDashboard, setToDashboard] = React.useState(false);

  if (toDashboard === true) {
    return <Navigate to="/dashboard" />;
  }

  return (
    <div>
      <h1>Register</h1>
      <Form afterSubmit={() => toDashboard(true)} />
    </div>
  );
}
```

---

## Imperative Navigation with `useNavigate`

React Router's [`useNavigate`](..//Router%20Hooks/useNavigate.md) hook grants access to navigate, enabling programmatic navigation. For example:

```jsx
import { useNavigate } from 'react-router-dom

function Register () {
  const navigate = useNavigate()

  return (
    <div>
      <h1>Register</h1>
      <Form afterSubmit={() => navigate('/dashboard')} />
    </div>
  )
}
```

[**Want to learn more?**](https://ui.dev/react-router-programmatically-navigate)
