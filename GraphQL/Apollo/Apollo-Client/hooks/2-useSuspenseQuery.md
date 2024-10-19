# `useSuspenseQuery` Apollo Clint Hook

To Suspense (UI feedback) to know more [you can see](../1-Fetching/1-Suspense.md)

**For Example:**

```jsx
// Create the main App component
function App() {
  // Wrap the List component within a Suspense boundary
  return (
    <Suspense fallback={<Spinner />}>
      {/* Display Spinner while data is fetched */}
      <List />
    </Suspense>
  );
}

// Create the List component that displays the fetched list
function List() {
  // Use useSuspenseQuery hook to fetch data and suspend rendering
  const { data } = useSuspenseQuery(listQuery);

  // Once data is available, render the list items
  return (
    <ol>
      {data.list.map((item) => (
        <Item key={item.id} id={item.id} />
      ))}
    </ol>
  );
}
```
