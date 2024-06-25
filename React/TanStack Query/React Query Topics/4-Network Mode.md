# Network Mode

TanStack Query offers three different network modes to control how **Queries** and **Mutations** behave in the absence of a network connection.

## Modes

### Online (Default)

In this mode, Queries and Mutations will only proceed if a network connection is available. If a fetch is initiated but cannot be completed due to no network connection, the query will remain in its current state (`pending`, `error`, `success`).

- **Key Points:**
  - Queries stay in their current state if no network connection is available.
  - `refetchOnReconnect` defaults to `true`, meaning queries will automatically retry once the network is restored.
  - Queries can be in a `paused` fetch status even if they are `pending`.

### Always

In this mode, Queries and Mutations will always fetch, ignoring the online/offline state. This mode is suitable for environments where an active network connection is not required for queries to work.

- **Key Points:**
  - Queries will never be `paused` due to no network connection.
  - Retries will proceed without pausing, and the query will go into `error` state if it fails.
  - `refetchOnReconnect` defaults to `false` because reconnecting is not a trigger for refetching stale queries.

### OfflineFirst

In this mode, TanStack Query attempts to fetch data once. If the data retrieval fails (e.g., due to no internet connection), retries are paused. This behavior is useful for offline-first Progressive Web Apps (PWAs) and HTTP caching with `Cache-Control` headers.

- **Key Points:**
  - Tries to fetch data once and pauses retries if it fails.
  - Suitable for offline-first PWAs that can use local caches.
  - Compatible with HTTP caching mechanisms to avoid unnecessary server requests.

## Use Cases

### Offline-First PWAs

- **Local Data Storage:** PWAs can store data locally using service workers. With `offlineFirst`, the query function might succeed by retrieving data from the local cache if available.
- **Cache Miss Handling:** If data is not cached, the query function will fail due to no internet, and retries will be paused to avoid unnecessary fetch attempts.

### HTTP Caching

- **Cache-Control Header:** Servers can use the `Cache-Control` header to instruct browsers to store data locally for a specified duration. With `offlineFirst`, the query function might use the cached data if it's still valid.
- **Retry Management:** If the cache is invalid or absent, the query function tries to fetch online but pauses retries after the first failure to prevent excessive requests.

## Example

Here's an example of how to use these network modes with TanStack Query:

```tsx
import {
  useQuery,
  QueryClient,
  QueryClientProvider,
} from "@tanstack/react-query";

// Create a query client
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      networkMode: "offlineFirst", // Set the default network mode
    },
  },
});

function fetchData() {
  // Example fetch function
  return fetch("/api/data").then((res) => res.json());
}

function MyComponent() {
  const { data, error, isLoading } = useQuery({
    queryKey: ["data"],
    queryFn: fetchData,
    networkMode: "online", // Override default network mode for this query
  });

  if (isLoading) return <span>Loading...</span>;
  if (error) return <span>Error: {error.message}</span>;

  return <div>{data}</div>;
}

export function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <MyComponent />
    </QueryClientProvider>
  );
}
```

In this example, the `MyComponent` query is set to use the `online` network mode, overriding the default `offlineFirst` mode specified in the `QueryClient` configuration.
