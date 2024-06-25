# Query Keys

Query keys are essential in identifying specific data for fetching, caching, and refetching logic in data management libraries like React Query. They must be serializable to JSON.

## Simple Query Key Example

A simple query key for fetching a list of todos.

```tsx
useQuery({ queryKey: ["todos"], queryFn: fetchTodoList });
```

## Query Keys with Variables

When fetching specific data based on parameters such as an ID or other identifiers, variables are included in query keys.

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

```tsx
function Todos({ todoId }) {
  // Fetch data based on a query key and query function
  const { data, error, isPending, isSuccess, isError } = useQuery({
    // The query key uniquely identifies this specific data fetch.
    // It's an array containing 'todos' and the `todoId`
    queryKey: ["todos", todoId],
    // This function defines how to fetch the data. It likely calls
    // another function `fetchTodoById` that takes the `todoId` as an argument
    queryFn: () => fetchTodoById(todoId),
  });

  // Add your component logic here
}
```
