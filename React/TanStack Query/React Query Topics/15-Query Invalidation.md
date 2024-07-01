# Query Invalidation

invalidation refers to the process of marking cached data from a query as potentially out-of-date. This doesn't remove the data, but tells React Query it might not reflect the latest information.

For Example:

```tsx
// Invalidate every query in the cache
queryClient.invalidateQueries();
// Invalidate every query with a key that starts with `todos`
queryClient.invalidateQueries({ queryKey: ["todos"] });
```

**When to Invalidate Queries:**

- **After Mutations:** When a mutation successfully updates data on the server, it's likely that related queries using that data are now outdated. Invalidate them to trigger a refetch and ensure UI consistency.
- **Manual Invalidation:** You can manually invalidate queries based on user actions or external events that might affect the data. For example, if a user logs out, you might invalidate queries that rely on user authentication.
