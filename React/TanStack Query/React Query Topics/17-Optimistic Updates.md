# Optimistic Updates in React Query

React Query provides two ways to optimistically update your UI before a mutation has completed:

1. **Using the `onMutate` Option:** Update your cache directly.
2. **Using the `variables` from `useMutation` Result:** Update your UI based on the returned `variables`.

## Example: Adding a Todo Item

Here’s a simple example demonstrating how to optimistically update the UI when adding a new todo item:

```tsx
const addTodoMutation = useMutation({
  // Define the mutation function
  mutationFn: (newTodo: string) => axios.post("/api/data", { text: newTodo }),

  // Ensure the mutation stays in `pending` state until the refetch is finished
  onSettled: async () => {
    // Invalidate the "todos" query to refetch the updated list
    return await queryClient.invalidateQueries({ queryKey: ["todos"] });
  },
});

// Destructure the mutation result to access its properties
const { isPending, submittedAt, variables, mutate, isError } = addTodoMutation;
```

You will then have access to `addTodoMutation.variables` to update your UI optimistically:

```tsx
<ul>
  {todoQuery.items.map((todo) => (
    // Render each todo item
    <li key={todo.id}>{todo.text}</li>
  ))}
  {isPending && (
    // Render the optimistically added todo item with reduced opacity
    <li style={{ opacity: 0.5 }}>{variables}</li>
  )}
</ul>
```

## Handling Mutations and Queries in Different Components

This approach works well if the mutation and the query are within the same component. However, if they reside in different components, you can access mutations in other components using the `useMutationState` hook. It is best combined with a `mutationKey`.

### Example: Accessing Variables in Different Components

```tsx
// Mutation definition somewhere in your app
const { mutate } = useMutation({
  // Define the mutation function
  mutationFn: (newTodo: string) => axios.post("/api/data", { text: newTodo }),

  // Invalidate the "todos" query to refetch the updated list
  onSettled: () => queryClient.invalidateQueries({ queryKey: ["todos"] }),

  // Assign a mutation key for easy identification
  mutationKey: ["addTodo"],
});

// Accessing variables in a different component
const variables = useMutationState<string>({
  // Filter to get the pending mutation with the specific mutation key
  filters: { mutationKey: ["addTodo"], status: "pending" },

  // Select the variables from the mutation state
  select: (mutation) => mutation.state.variables,
});

// Define a query to fetch todos
const todoQuery = useQuery({
  queryKey: ["todos"],
  queryFn: () => axios.get("/api/todos").then((res) => res.data),
});

// Use the variables to optimistically update the UI in the different component
return (
  <ul>
    {todoQuery.items.map((todo) => (
      // Render each todo item
      <li key={todo.id}>{todo.text}</li>
    ))}
    {variables && (
      // Render the optimistically added todo item with reduced opacity
      <li style={{ opacity: 0.5 }}>{variables}</li>
    )}
  </ul>
);
```
