# Query Retries

In TanStack Query, when a query fails (i.e., the query function throws an error), it automatically retries the query based on the configured retry logic. The default number of retry attempts is `3`, but you can customize this behavior.

## Example: Custom Retry Count

```tsx
import { useQuery } from "@tanstack/react-query";

// Configure a specific query to retry up to 10 times
const result = useQuery({
  queryKey: ["todos", 1],
  queryFn: fetchTodoListPage,
  retry: 10, // Retry failed requests 10 times before showing an error
});
```

## Retry Delay

Retries in TanStack Query do not occur immediately after a request fails. Instead, a back-off delay is applied, which increases exponentially with each attempt, but is capped at 30 seconds.

### Example: Custom Retry Delay

You can customize the retry delay globally through the `QueryClient` configuration:

```tsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

// Configure the retry delay logic
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      retryDelay: (attemptIndex) => Math.min(1000 * 2 ** attemptIndex, 30000),
    },
  },
});
```

In this example, the retry delay starts at 1000ms and doubles with each retry attempt, capping at a maximum of 30000ms (30 seconds).

By configuring the `retry` and `retryDelay` options, you can fine-tune the retry behavior of your queries to improve resilience and provide a better user experience.
