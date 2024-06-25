# Query Function

A query function in TanStack Query can be any function that **returns a promise**. This promise should either **resolve with the data** or **throw an error**.

## Error Handling & Throwing

To signal an error to TanStack Query, the query function **must throw** or return a **rejected Promise**. Any error thrown in the query function will be reflected in the query's `error` state.

---

## Query Options

Using the `queryOptions` helper is an efficient way to share `queryKey` and `queryFn` between multiple places while keeping them co-located. This approach is particularly beneficial when using **TypeScript** as it provides type inference and type safety.

### Example

```tsx
import { queryOptions } from "@tanstack/react-query";

// Define query options for fetching groups
function groupOptions(id: number) {
  return queryOptions({
    queryKey: ["groups", id], // Unique query key with group ID
    queryFn: () => fetchGroups(id), // Function to fetch groups by ID
    staleTime: 5 * 1000, // Time (in milliseconds) the data is considered fresh
  });
}

// Usage examples
useQuery(groupOptions(1)); // Using query options with useQuery
useSuspenseQuery(groupOptions(5)); // Using query options with useSuspenseQuery
useQueries({
  queries: [groupOptions(1), groupOptions(2)], // Using query options with useQueries
});
queryClient.prefetchQuery(groupOptions(23)); // Prefetching query using query options
queryClient.setQueryData(groupOptions(42).queryKey, newGroups); // Setting query data manually
```

By defining and using query options in this way, you can maintain consistency, improve code reusability, and leverage TypeScript's type safety in your TanStack Query implementations.
