# Background Fetching Indicators

A query's `status === 'pending'` state is sufficient to show the initial hard-loading state for a query, but sometimes you may want to display an additional indicator that a query is refetching in the background. To do this, queries also provide an `isFetching` boolean that you can use to show that it's in a fetching state.

### Example

```tsx
const {
  status, // Status of the query (e.g., 'pending', 'success', 'error')
  data: todos, // Data returned from the query
  error, // Error returned from the query (if any)
  isFetching, // Boolean indicating if the query is currently fetching data
} = useQuery({
  queryKey: ["todos"], // Unique key for the query
  queryFn: fetchTodos, // Function to fetch the todos data
});
```

## Displaying Global Background Fetching Loading State

In addition to individual query loading states, if you would like to show a global loading indicator when any queries are fetching (including in the background), you can use the `useIsFetching` hook:

### Example

```tsx
function GlobalLoadingIndicator() {
  const isFetching = useIsFetching(); // Hook to check if any query is fetching

  return isFetching ? (
    <div>Queries are fetching in the background...</div> // Display loading indicator if any query is fetching
  ) : null; // Otherwise, render nothing
}
```

By using these indicators, you can provide a better user experience by clearly showing when data is being fetched, both at the individual query level and globally across your application.
