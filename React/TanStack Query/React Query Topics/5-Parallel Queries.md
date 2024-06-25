# Parallel Queries

Parallel queries are executed simultaneously to maximize data fetching concurrency. TanStack Query offers robust solutions to handle both static and dynamic parallel queries effectively.

## Types of Parallel Queries

### Manual Parallel Queries

When the number of parallel queries is fixed, you can effortlessly utilize manual parallel queries. Simply use multiple instances of TanStack Query's `useQuery` and `useInfiniteQuery` hooks side-by-side. This approach does not require additional setup.

```tsx
import { useQuery } from "@tanstack/react-query";

function App() {
  const todosQuery = useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodos,
  });

  const usersQuery = useQuery({
    queryKey: ["users"],
    queryFn: fetchUsers,
  });

  if (todosQuery.isLoading || usersQuery.isLoading) {
    return <span>Loading...</span>;
  }

  if (todosQuery.isError || usersQuery.isError) {
    return (
      <span>Error: {todosQuery.error.message || usersQuery.error.message}</span>
    );
  }

  return (
    <div>
      <h1>Todos</h1>
      <ul>
        {todosQuery.data.map((todo) => (
          <li key={todo.id}>{todo.title}</li>
        ))}
      </ul>

      <h1>Users</h1>
      <ul>
        {usersQuery.data.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

### Dynamic Parallel Queries with `useQueries`

For scenarios where the number of queries changes from render to render, manual querying isn't suitable as it would violate React's rules of hooks. In such cases, TanStack Query provides the `useQueries` hook. This hook allows you to dynamically execute as many parallel queries as needed.

```tsx
import { useQueries } from "@tanstack/react-query";

function App({ users }) {
  const userQueries = useQueries({
    queries: users.map((user) => ({
      queryKey: ["user", user.id],
      queryFn: () => fetchUserById(user.id),
    })),
  });

  return (
    <div>
      {userQueries.map((query, index) => {
        if (query.isLoading)
          return <span key={index}>Loading user {users[index].id}...</span>;
        if (query.isError)
          return (
            <span key={index}>
              Error loading user {users[index].id}: {query.error.message}
            </span>
          );

        return (
          <div key={index}>
            <h3>{query.data.name}</h3>
            <p>{query.data.email}</p>
          </div>
        );
      })}
    </div>
  );
}
```

### Handling Parallel Queries in Suspense Mode

When using React Query in suspense mode, the typical pattern of parallelism can cause issues. The first query may throw a promise internally, causing the component to suspend before the remaining queries run. To overcome this, you can either use the `useSuspenseQueries` hook (recommended) or manage parallelism manually with separate components for each `useSuspenseQuery` instance.

```tsx
import { useSuspenseQuery } from "@tanstack/react-query";

function UserComponent({ userId }) {
  const { data } = useSuspenseQuery({
    queryKey: ["user", userId],
    queryFn: () => fetchUserById(userId),
  });

  return (
    <div>
      <h3>{data.name}</h3>
      <p>{data.email}</p>
    </div>
  );
}

function App({ users }) {
  return (
    <div>
      {users.map((user) => (
        <React.Suspense
          key={user.id}
          fallback={<span>Loading user {user.id}...</span>}
        >
          <UserComponent userId={user.id} />
        </React.Suspense>
      ))}
    </div>
  );
}
```

By leveraging these approaches, you can efficiently handle both static and dynamic parallel data fetching scenarios, ensuring your application remains performant and responsive.
