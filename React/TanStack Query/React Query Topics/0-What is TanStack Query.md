# What is TanStack Query

TanStack Query **(FKA React Query)** is often described as the missing data-fetching library for web applications, but in more technical terms, it makes **fetching**, **caching**, **synchronizing** and **updating** server state in your web applications a breeze.

---

## Important Defaults in TanStack Query

TanStack Query is configured with aggressive but sensible defaults. Understanding these defaults is crucial to avoid unexpected behavior and ease debugging. Here’s a breakdown of these important defaults:

### Stale Data

1. **Cached Data Considered Stale:**
   - By default, data fetched by `useQuery` or `useInfiniteQuery` is considered stale.
   - **Configuring `staleTime`:**
     - You can change this behavior globally or per-query using the `staleTime` option.
     - Setting a longer `staleTime` means queries won’t refetch their data as frequently.

### Automatic Refetching

2. **Stale Queries Refetched Automatically:**
   - **When New Instances Mount:**
     - New instances of a query automatically refetch if the data is stale.
   - **Window Refocused:**
     - Queries refetch when the browser window is refocused.
   - **Network Reconnected:**
     - Queries refetch when the network connection is restored.
   - **Optional Refetch Interval:**
     - Queries can be configured with a `refetchInterval` to periodically refetch data.
   - **Configuring Refetch Options:**
     - Use options like `refetchOnMount`, `refetchOnWindowFocus`, `refetchOnReconnect`, and `refetchInterval` to change this functionality.

### Inactive Queries

3. **Inactive Query Garbage Collection:**
   - Queries with no active instances are labeled as "inactive" and remain in the cache for potential reuse.
   - **Default Garbage Collection Time:**
     - By default, inactive queries are garbage collected after 5 minutes (1000 _ 60 _ 5 milliseconds).
   - **Configuring `gcTime`:**
     - Alter the default `gcTime` to change the duration before inactive queries are removed from the cache.

### Query Failure and Retry

4. **Retrying Failed Queries:**
   - Queries that fail are silently retried 3 times with exponential backoff before showing an error.
   - **Configuring Retry Behavior:**
     - Change the default `retry` and `retryDelay` options to customize the retry attempts and delay.

### Structural Sharing

5. **Structural Sharing of Query Results:**
   - By default, TanStack Query uses structural sharing to detect if data has changed. If not, it keeps the data reference unchanged, aiding performance with hooks like `useMemo` and `useCallback`.
   - **JSON-Compatible Values:**
     - Structural sharing works with JSON-compatible values. Non-JSON-compatible values are always considered changed.
   - **Disabling Structural Sharing:**
     - If you face performance issues, such as with large responses, disable structural sharing using the `config.structuralSharing` flag.
   - **Custom Structural Sharing Function:**
     - For non-JSON-compatible values, you can provide a custom function via `config.structuralSharing` to determine if data has changed and retain references as needed.

Understanding and configuring these defaults can help you leverage the full power of TanStack Query while avoiding potential pitfalls. Adjust these settings based on your application’s requirements to achieve optimal performance and user experience.
