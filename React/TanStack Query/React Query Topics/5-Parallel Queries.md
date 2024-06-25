# Parallel Queries

Parallel queries are executed simultaneously to maximize data fetching concurrency. TanStack Query offers robust solutions to handle both static and dynamic parallel queries effectively.

## Types of Parallel Queries

### Manual Parallel Queries

When the number of parallel queries is fixed, you can effortlessly utilize manual parallel queries. Simply use multiple instances of TanStack Query's `useQuery` and `useInfiniteQuery` hooks side-by-side. This approach does not require additional setup.

### Dynamic Parallel Queries with `useQueries`

For scenarios where the number of queries changes from render to render, manual querying isn't suitable as it would violate React's rules of hooks. In such cases, TanStack Query provides the `useQueries` hook. This hook allows you to dynamically execute as many parallel queries as needed.

### Example

```tsx
function App({ users }) {
  const userQueries = useQueries({
    queries: users.map((user) => ({
      queryKey: ["user", user.id],
      queryFn: () => fetchUserById(user.id),
    })),
  });
}
```

### Handling Parallel Queries in Suspense Mode

When using React Query in suspense mode, the typical pattern of parallelism can cause issues. The first query may throw a promise internally, causing the component to suspend before the remaining queries run. To overcome this, you can either use the `useSuspenseQueries` hook (recommended) or manage parallelism manually with separate components for each `useSuspenseQuery` instance.

By leveraging these approaches, you can efficiently handle both static and dynamic parallel data fetching scenarios, ensuring your application remains performant and responsive.
