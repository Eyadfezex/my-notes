# Prefetching

The goal of prefetching is to make data fetch before the user navigates to a page or attempts to load some known content.

situations that you may want to do this, but some very common use cases are:

1. User hovers over a navigation element
2. User hovers over a list element that is a link
3. User hovers over a next pagination button
4. User navigates to a page and you know that some components down the tree will require said data. This way, you can prevent fetching waterfalls.

**Customizing the Hook Behavior**
You can specify these prefetch options when declaring the hook or at the call site. The call site will take priority over the defaults.

- `ifOlderThan` - (default: `false` | `number`) - number is value in seconds
  If specified, it will only run the query if the difference between `new Date()` and the last `fulfilledTimeStamp` is greater than the given value
- `force`
  If `force: true`, it will ignore the `ifOlderThan` value if it is set and the query will be run even if it exists in the cache.
  Sure, here's a condensed version:

---

The trigger function returns void and governs query behavior as follows:

- Setting `force: true` ensures the query runs regardless, except if the same query is already in-flight.
- If no options are specified and the query exists in the cache, it won't be performed; otherwise, it executes.
- With `ifOlderThan`, if false and the query is in the cache, it's not performed; if true, it executes even with existing cache data.

Example:

```jsx
function User() {
  const prefetchUser = usePrefetch("getUser");

  // Low priority hover fires only if last request was >35s ago; high priority always fires.

  return (
    <div>
      <button onMouseEnter={() => prefetchUser(4, { ifOlderThan: 35 })}>
        Low priority
      </button>
      <button onMouseEnter={() => prefetchUser(4, { force: true })}>
        High priority
      </button>
    </div>
  );
}
```

This succinctly outlines the trigger function's behavior and demonstrates its use with the `usePrefetch` hook.
