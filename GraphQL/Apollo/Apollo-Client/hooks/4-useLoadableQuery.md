# `useLoadableQuery` Apollo Clint Hook

A hook for imperatively loading a query, such as responding to a user interaction

**For Example:**

```jsx
function App() {
  // Use useLoadableQuery to fetch data with GET_GREETING automatically on mount
  // and suspend rendering until the query completes.
  const [loadGreeting, queryRef] = useLoadableQuery(GET_GREETING);

  return (
    <>
      {/* Button to manually trigger the greeting fetch if desired */}
      <button onClick={() => loadGreeting({ language: "english" })}>
        Load greeting
      </button>
      {/* Wrap Hello component with Suspense for loading state handling */}
      <Suspense fallback={<div>Loading...</div>}>
        {queryRef && <Hello queryRef={queryRef} />}
        {/* Render Hello only if data is available */}
      </Suspense>
    </>
  );
}

// Create the Hello component to display the fetched greeting
function Hello({ queryRef }) {
  // Use useReadQuery to access the data fetched with the provided query reference
  const { data } = useReadQuery(queryRef);

  // Render the greeting message if data is available
  return <div>{data.greeting.message}</div>;
}
```
