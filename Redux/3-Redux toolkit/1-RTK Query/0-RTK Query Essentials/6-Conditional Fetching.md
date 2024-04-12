# Conditional Fetching

**Problem:**
Query hooks automatically begin fetching data as soon as the component is mounted. But, there are use cases where you may want to delay fetching data until some condition becomes true.

**Solution:**

- Using `skip` parameter in a hook
- Using `Lazy` Query hook

**`skip` Example:**

```js
const Pokemon = ({ name, skip }: { name: string; skip: boolean }) => {
  // Destructure the response from the useGetPokemonByNameQuery hook
  const { data, error, status } = useGetPokemonByNameQuery(name, {
    skip,
  });

  return (
    <div>
      {/* Display Pokemon name */}
      {name} - 

      {/* Conditionally display fetch status based on query result */}
      {status === 'loading' && <span>Loading...</span>}
      {status === 'success' && data && <span>Fetched!</span>}
      {status === 'error' && error && <span>Error: {error.message}</span>}
    </div>
  );
};

```
