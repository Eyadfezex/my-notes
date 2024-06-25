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
    queryKey: ["groups", id],
    queryFn: () => fetchGroups(id),
    staleTime: 5 * 1000,
  });
}

// Usage examples
useQuery(groupOptions(1));
useSuspenseQuery(groupOptions(5));
useQueries({
  queries: [groupOptions(1), groupOptions(2)],
});
queryClient.prefetchQuery(groupOptions(23));
queryClient.setQueryData(groupOptions(42).queryKey, newGroups);
```
