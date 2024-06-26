# Window Focus Refetching in TanStack Query

TanStack Query automatically refetches query data in the background when the window is refocused, provided the data is stale. This ensures your application always displays the most up-to-date information when users return to it.

## Disabling Window Focus Refetching

You can disable this feature either globally for all queries or on a per-query basis.

### Disabling Globally

To disable window focus refetching for all queries in your application, set the `refetchOnWindowFocus` option to `false` in the `QueryClient` configuration.

```tsx
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      refetchOnWindowFocus: false, // default is true
    },
  },
});
```

### Disabling Per-Query

To disable window focus refetching for a specific query, set the `refetchOnWindowFocus` option to `false` in the `useQuery` hook configuration.

```tsx
useQuery({
  queryKey: ["todos"],
  queryFn: fetchTodos,
  refetchOnWindowFocus: false,
});
```

## Managing the Focus State

TanStack Query provides a `focusManager` to manually control the focus state. This is useful if you need to override the default focus behavior programmatically.

```tsx
import { focusManager } from "@tanstack/react-query";

// Manually set the focus state to focused
focusManager.setFocused(true);

// Reset to the default focus state check
focusManager.setFocused(undefined);
```

By understanding and configuring the `refetchOnWindowFocus` option, you can better control the behavior of your queries and ensure that your application performs optimally according to your specific needs.
