# Queries with React Query

React Query simplifies data fetching in React applications by managing cache, synchronization, and updating data. Here's an overview of using queries effectively with React Query.

## Basic Query Example

To fetch data using React Query, use the `useQuery` hook. This hook takes two main arguments: a unique key and a function that returns a promise resolving to the data.

### Simple Example

```tsx
import { useQuery } from "@tanstack/react-query";

function App() {
  const { data, error, isPending, isSuccess, isError } = useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodoList,
  });

  // Add your component logic here
}
```

### Detailed Example

```tsx
import { useQuery } from "@tanstack/react-query";

// Function to fetch todo list data (replace with your implementation)
const fetchTodoList = async () => {
  const response = await fetch("/api/todos");
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
};

// This function component renders the list of todos
function Todos() {
  // Fetches todo list data using the useQuery hook
  const { isPending, isError, data, error } = useQuery({
    // Query key to identify the specific data being fetched
    queryKey: ["todos"],
    // Function responsible for fetching the todo list data
    queryFn: fetchTodoList,
  });

  // Display loading message while data is being fetched
  if (isPending) {
    return <span>Loading...</span>;
  }

  // Display error message if data fetching fails
  if (isError) {
    return <span>Error: {error.message}</span>;
  }

  // Display the fetched data
  return (
    <ul>
      {data.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```

## Handling Query States

The result object from `useQuery` provides several important states to handle:

- `isPending` or `state === 'pending'`: The query has no data yet and is loading.
- `isSuccess` or `state === 'success'`: The query has successfully fetched the data.
- `isError` or `state === 'error'`: The query encountered an error during fetching.

### Example with State Handling

```tsx
function Todos() {
  const { isPending, isError, data, error } = useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodoList,
  });

  if (isPending) {
    return <span>Loading...</span>;
  }

  if (isError) {
    return <span>Error: {error.message}</span>;
  }

  return (
    <ul>
      {data.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```

By following these examples, you can effectively manage data fetching in your React applications using React Query, ensuring a seamless and responsive user experience.
