# useParams

`useParams` in React Router gets dynamic values from the URL, like :id from /users/:id. Child routes inherit these values from their parent routes.

## Syntax

```jsx
function ProfilePage() {
  // Get the userId param from the URL.
  let { userId } = useParams();
  // ...
}

function App() {
  return (
    <Routes>
      <Route path="users">
        <Route path=":userId" element={<ProfilePage />} />
        <Route path="me" element={...} />
      </Route>
    </Routes>
  );
}
```
