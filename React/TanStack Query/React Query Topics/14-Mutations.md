# Mutations

Mutations are typically used to create, update, or delete data, or to perform server-side effects. TanStack Query provides a `useMutation` hook for this purpose.

## Example of Using `useMutation`

```tsx
function App() {
  const mutation = useMutation({
    mutationFn: (newTodo) => {
      return axios.post("/todos", newTodo);
    },
  });

  return (
    <div>
      {mutation.isPending ? (
        "Adding todo..."
      ) : (
        <>
          {mutation.isError ? (
            <div>An error occurred: {mutation.error.message}</div>
          ) : null}

          {mutation.isSuccess ? <div>Todo added!</div> : null}

          <button
            onClick={() => {
              mutation.mutate({ id: new Date(), title: "Do Laundry" });
            }}
          >
            Create Todo
          </button>
        </>
      )}
    </div>
  );
}
```

## Resetting Mutation State

You can clear the `data` or `error` of the mutation request using the `reset` function. This is useful to reset the state after handling errors or successfully completing an action.

### Example of Resetting Mutation State

```tsx
const CreateTodo = () => {
  const [title, setTitle] = useState("");
  const mutation = useMutation({ mutationFn: createTodo });

  const onCreateTodo = (e) => {
    e.preventDefault();
    mutation.mutate({ title });
  };

  return (
    <form onSubmit={onCreateTodo}>
      {mutation.error && (
        <h5 onClick={() => mutation.reset()}>{mutation.error}</h5>
      )}
      <input
        type="text"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
      />
      <br />
      <button type="submit">Create Todo</button>
    </form>
  );
};
```

### Key Points

- **`useMutation`**: Hook for handling mutations in TanStack Query.
- **`mutationFn`**: Function that defines the mutation logic.
- **`mutation.isPending`**: Boolean indicating if the mutation is in progress.
- **`mutation.isError`**: Boolean indicating if there was an error with the mutation.
- **`mutation.isSuccess`**: Boolean indicating if the mutation was successful.
- **`mutation.mutate`**: Function to trigger the mutation.
- **`mutation.reset`**: Function to reset the mutation state.
