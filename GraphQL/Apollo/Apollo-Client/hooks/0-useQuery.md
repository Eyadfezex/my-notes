# `useQuery` Apollo Clint Hook

A hook for executing queries in an Apollo application.

When your component renders, `useQuery` returns an object from Apollo Client that contains `loading`, `error`, and `data` properties you can use to render your UI.

**for Example:**

```jsx
// Create a React component named Hello
function Hello() {
  // Use the useQuery hook to execute the GET_GREETING query
  const { loading, error, data } = useQuery(GET_GREETING, {
    // Provide the 'language' variable with a value of 'english'
    variables: { language: "english" },
  });

  // Display a loading message while the query is being fetched
  if (loading) return <p>Loading ...</p>;

  // If there's an error fetching the data, display an error message
  if (error) return <p>Error: {error.message}</p>;

  // Extract the greeting message from the query response
  const greetingMessage = data?.greeting?.message;

  // Render the greeting message if data is available
  return <h1>Hello {greetingMessage}!</h1>;
}
```
