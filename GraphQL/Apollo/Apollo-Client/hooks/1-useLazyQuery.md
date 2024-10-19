# `useLazyQuery` Apollo Clint Hook

A hook for imperatively executing queries in an Apollo application, in response to user interaction.

**Fore Example:**

```jsx
// Create a React component named Hello
function Hello() {
  // Use the useLazyQuery hook to execute the GET_GREETING query on demand
  const [loadGreeting, { called, loading, data }] = useLazyQuery(
    GET_GREETING,
    { variables: { language: "english" } } // Pre-define language variable
  );

  // Check if the query has been called (button clicked) and is still loading
  if (called && loading) return <p>Loading ...</p>;

  // If the query hasn't been called, display a button to initiate the fetch
  if (!called) {
    return <button onClick={() => loadGreeting()}>Load greeting</button>;
  }

  // If the query has been called and data is available, display the greeting
  return <h1>Hello {data.greeting.message}!</h1>;
}
```
