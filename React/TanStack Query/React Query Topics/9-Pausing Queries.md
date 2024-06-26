# Disabling/Pausing Queries in TanStack Query

To disable a query from automatically running, use the `enabled` option. This option can be set to `false` or accept a callback that returns a boolean.

## When `enabled` is `false`

- If the query has cached data, it will initialize with `status === 'success'` or `isSuccess`.
- If the query has no cached data, it will start with `status === 'pending'` and `fetchStatus === 'idle'`.
- The query will not fetch automatically on mount.
- The query will not refetch in the background.
- The query will ignore query client `invalidateQueries` and `refetchQueries` calls.
- The `refetch` function from `useQuery` can manually trigger the query to fetch (it will not work with `skipToken`).

### Example: Disabling a Query

```tsx
function Todos() {
  const { isLoading, isError, data, error, refetch, isFetching } = useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodoList,
    enabled: false, // Query is disabled
  });

  return (
    <div>
      {isFetching && <span>Loading...</span>}
      {isError && <span>Error: {error.message}</span>}
      {data && <TodosList data={data} />}
      <button onClick={() => refetch()}>Refetch Todos</button>
    </div>
  );
}
```

Disabling a query permanently is not the idiomatic way and opts out of many features like background refetches. It also shifts from a declarative approach to an imperative mode. For a more flexible approach, you can use lazy queries.

## Lazy Queries

The `enabled` option can be toggled to enable or disable a query based on certain conditions, such as user input.

### Example: Lazy Queries with Filters

```tsx
function Todos() {
  const [filter, setFilter] = React.useState("");

  const { data, isLoading, isFetching } = useQuery({
    queryKey: ["todos", filter],
    queryFn: () => fetchTodos(filter),
    enabled: !!filter, // Disabled if filter is empty
  });

  return (
    <div>
      <FiltersForm onApply={setFilter} />
      {isLoading && <span>Loading...</span>}
      {data && <TodosTable data={data} />}
    </div>
  );
}
```

## Handling Loading State

Lazy queries will be in `status: 'pending'` initially because there is no data yet. However, since the query is not enabled, you might not be able to use this flag to show a loading spinner. Use the `isLoading` flag instead, which is derived from:

`isPending && isFetching`

It will only be `true` if the query is currently fetching for the first time.

By understanding and utilizing the `enabled` option and lazy queries, you can control when queries run and manage their loading states effectively in your application.
