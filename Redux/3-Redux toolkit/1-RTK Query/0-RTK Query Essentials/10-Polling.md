# Polling

**Polling Overview**
In data fetching scenarios, polling allows you to simulate real-time updates by periodically re-executing a query at a predefined interval. This is particularly useful when the data source you're querying doesn't natively push updates (e.g., websockets, server-sent events), for example:

```tsx
import * as React from "react";
import { useGetPokemonByNameQuery } from "./services/pokemon";

export const Pokemon = ({ name }: { name: string }) => {
  // Automatically refetch every 3s unless the window is out of focus
  const { data, status, error, refetch } = useGetPokemonByNameQuery(name, {
    pollingInterval: 3000,
    skipPollingIfUnfocused: true,
  });

  return <div>{data}</div>;
};
```

---

**Best Practices and Considerations:**

- **Choose the Right Interval:** Balance between update frequency and potential server overload. Too frequent polling can strain server resources.
- **Network Conditions:** Account for network latency, which can further delay updates.
- **Data Sensitivity:** Don't poll for highly sensitive data unnecessarily.
- **Component Lifecycle:** Manage polling start/stop based on component visibility to avoid unnecessary fetches when the component isn't active.
