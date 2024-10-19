# Initial Query Data

## Setting Initial Data for a Query

To set initial data for a query, use the `initialData` option to prepopulate the query's cache if it is empty. This can improve the user experience by providing immediate data while waiting for the actual fetch to complete.

### Example of Using `initialData` to Prepopulate a Query

_Important: Since `initialData` is persisted to the cache, avoid providing placeholder, partial, or incomplete data. Instead, use `placeholderData` for temporary data._

```tsx
const result = useQuery({
  queryKey: ["todos"],
  queryFn: () => fetch("/todos"),
  initialData: initialTodos,
});
```

## Providing Initial Data from Cache

You can provide initial data for a query using cached results from another query. This is useful when you want to leverage existing cached data to reduce loading times and improve performance.

### Example of Providing Initial Data from Another Cached Result

```tsx
const result = useQuery({
  queryKey: ["todo", todoId],
  queryFn: () => fetch(`/todos/${todoId}`),
  initialData: () => {
    // Use a todo from the 'todos' query as the initial data for this specific todo query
    return queryClient.getQueryData(["todos"])?.find((d) => d.id === todoId);
  },
});
```

### Key Points

- **`initialData`**: Data or a function to provide initial data for the query. If a function is used, it can return data from another cached query.
