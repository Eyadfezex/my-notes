# Query Keys

Query keys are essential in identifying specific data for fetching, caching, and refetching logic in data management libraries like React Query. They must be serializable to JSON.

## Simple Query Key Example

A simple query key for fetching a list of todos.

```tsx
useQuery({ queryKey: ["todos"], queryFn: fetchTodoList });
```

## Query Keys with Variables

When fetching specific data based on parameters such as an ID or other identifiers, variables are included in query keys.

### Examples

```tsx
// Fetching an individual todo by ID
useQuery({ queryKey: ["todo", 5], queryFn: () => fetchTodoById(5) });

// Fetching a preview of an individual todo
useQuery({
  queryKey: ["todo", 5, { preview: true }],
  queryFn: () => fetchTodoPreviewById(5),
});

// Fetching a list of todos that are marked as "done"
useQuery({ queryKey: ["todos", { type: "done" }], queryFn: fetchDoneTodos });
```

## Dependent Query Keys

When a query depends on a variable, it should be included in the query key to ensure the fetch is correctly identified and managed.

### Example

```tsx
function Todos({ todoId }) {
  // Fetch data based on a query key and query function
  const { data, error, isPending, isSuccess, isError } = useQuery({
    // The query key uniquely identifies this specific data fetch
    queryKey: ["todos", todoId],
    // This function defines how to fetch the data
    queryFn: () => fetchTodoById(todoId),
  });

  if (isPending) {
    return <span>Loading...</span>;
  }

  if (isError) {
    return <span>Error: {error.message}</span>;
  }

  return (
    <div>
      <h3>{data.title}</h3>
      <p>{data.description}</p>
    </div>
  );
}
```

By utilizing query keys effectively, you can ensure precise data fetching, caching, and refetching behavior in your React applications using React Query.
