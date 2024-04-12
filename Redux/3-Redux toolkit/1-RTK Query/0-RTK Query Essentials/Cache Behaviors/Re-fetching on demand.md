# Re-fetching on demand

In order to achieve complete granular control over re-fetching data, you can use the `refetch` function returned as a result property from a `useQuery` or `useQuerySubscription` hook.

Calling the refetch function will force refetch the associated query.

Alternatively, you can dispatch the `initiate` thunk action for an endpoint, passing the option `forceRefetch: true` to the thunk action creator for the same effect.

```js
function handleRefetchOne() {
  // force re-fetches the data
  refetch();
}
```

## Or

```js
function handleRefetchTwo() {
  // has the same effect as `refetch` for the associated query
  dispatch(
    api.endpoints.getPosts.initiate(
      { count: 5 },
      { subscribe: false, forceRefetch: true }
    )
  );
}
```
