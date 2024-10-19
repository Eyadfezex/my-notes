# GraphQL Queries with Apollo Client in React

Fetch data with the useQuery hook

Executing a query with `useQuery` hook is the primary way, to run a query with React component do this:

```jsx
// Import necessary hooks from the @apollo/client library
import { gql, useQuery } from "@apollo/client";

// Define the GraphQL query named GET_DOGS
const GET_DOGS = gql`
  # This is a GraphQL query named GetDogs
  query GetDogs {
    # Request the dogs data from the server
    dogs {
      # Specify the fields you want to retrieve for each dog
      id
      breed
    }
  }
`;

// Functional React component named Dogs
function Dogs({ onDogSelected }) {
  // Use the useQuery hook to execute the GET_DOGS query
  // and destructure the response object into loading, error, and data properties
  const { loading, error, data } = useQuery(GET_DOGS);

  // Display "Loading..." while data is being fetched
  if (loading) return "Loading...";

  // Display error message if there's an error during data fetching
  if (error) return `Error! ${error.message}`;

  // Render the select element with dog breeds as options
  return (
    <select name="dog" onChange={onDogSelected}>
      {/* Map through the retrieved dogs data and render options */}
      {data.dogs.map((dog) => (
        <option key={dog.id} value={dog.breed}>
          {/* Display the breed name for each option */}
          {dog.breed}
        </option>
      ))}
    </select>
  );
}
```

---

## Caching response

Whenever Apollo Client fetches query results from your server, it **automatically** caches those results locally. This makes later executions of that same query extremely fast.

```jsx
// This constant defines a GraphQL query named GET_DOG_PHOTO.
// It uses a template literal with backticks (` `) for readability.
const GET_DOG_PHOTO = gql`
  # This query fetches data about a dog of a specific breed.
  query Dog($breed: String!) {
    # The 'dog' field requests data from the 'dog' endpoint on the server.
    # It takes a variable named 'breed' of type String (required!) as input.
    dog(breed: $breed) {
      # The 'id' field retrieves the dog's unique identifier.
      id
      # The 'displayImage' field retrieves the URL of the dog's image suitable for display.
      displayImage
    }
  }
`;

function DogPhoto({ breed }) {
  // This hook from Apollo Client (useQuery) fetches data based on the provided query (GET_DOG_PHOTO)
  // and variables ({ breed }).
  //   breed variable get from GET_DOGS query cached data
  const { loading, error, data } = useQuery(GET_DOG_PHOTO, {
    variables: { breed },
  });

  // If the data is still loading, return null to avoid rendering incomplete content.
  if (loading) return null;

  // If there's an error fetching the data, display an error message.
  if (error) return `Error! ${error}`;

  // If data is fetched successfully, return an image component using the dog's displayImage URL.
  // Set the image dimensions (height and width) to 100 pixels each using inline styles.
  return (
    <img src={data.dog.displayImage} style={{ height: 100, width: 100 }} />
  );
}
```

---

## Updating cached query results

Apollo Client supports two strategies for Updating cached query results: polling and refetching.

### polling

To enable polling for a query, pass a pollInterval configuration option to the useQuery hook with an interval in milliseconds:

```jsx
function DogPhoto({ breed }) {
  // 'pollInterval: 500' sets the polling interval to 500 milliseconds, meaning it will refetch the data every half a second.
  const { loading, error, data } = useQuery(GET_DOG_PHOTO, {
    variables: { breed },
    pollInterval: 500,
  });

  if (loading) return null;

  if (error) return `Error! ${error}`;

  return (
    <img src={data.dog.displayImage} style={{ height: 100, width: 100 }} />
  );
}
```

### Refetching

Refetching enables you to refresh query results in response to a particular user action, as opposed to using a fixed interval.

for example:

```jsx
function DogPhoto({ breed }) {
  const { loading, error, data, refetch } = useQuery(GET_DOG_PHOTO, {
    variables: { breed },
  });

  if (loading) return null;

  if (error) return `Error! ${error}`;

  // Data fetched successfully, return the component with image and refetch button
  return (
    <div>
      <img src={data.dog.displayImage} style={{ height: 100, width: 100 }} />
      <button onClick={() => refetch()}>
        {/* Refetches data when clicked */}
        Refetch new breed!
      </button>
    </div>
  );
}
```

If you use a variables in query you can provide a **new one** to refetch, for example:

```jsx
<button
  onClick={() =>
    refetch({
      breed: "dalmatian", // Always refetches a dalmatian instead of original breed
    })
  }
>
  Refetch!
</button>
```

---

## Inspecting loading & error states

### loading states

The useQuery hook's result object provides fine-grained information about the status of the query via the networkStatus property. To take advantage of this information, we set the notifyOnNetworkStatusChange option to true so our query component re-renders while a refetch is in flight:

```jsx
import { NetworkStatus } from "@apollo/client"; // Import NetworkStatus enum from Apollo Client

function DogPhoto({ breed }) {
  // Destructure the result object from useQuery hook
  const { loading, error, data, refetch, networkStatus } = useQuery(
    GET_DOG_PHOTO, // Replace with your actual GraphQL query
    {
      variables: { breed },
      notifyOnNetworkStatusChange: true, // Enable notifications on network status change
    }
  );

  // Handle refetching state
  if (networkStatus === NetworkStatus.refetch) return "Refetching!";

  // Handle loading state
  if (loading) return null;

  // Handle error state
  if (error) return `Error! ${error}`;

  // Display dog image and refetch button
  return (
    <div>
      <img src={data.dog.displayImage} style={{ height: 100, width: 100 }} />
      <button onClick={() => refetch()}>Refetch!</button>
    </div>
  );
}
```

### error states

You can customize your query error handling by providing the errorPolicy configuration option to the useQuery hook. The default value is none, which tells Apollo Client to treat all GraphQL errors as runtime errors. In this case, Apollo Client discards any query response data returned by the server and sets the error property in the useQuery result object.

---

## Manual execution with `useLazyQuery`

if you want to execute a query in response to a different event, such as a user clicking a button, we use something called `useLazyQuery`, for example:

```jsx
// Import the GraphQL query for fetching dog photos (replace with your actual query)
const GET_DOG_PHOTO = gql`
  # Write your GraphQL query here to fetch dog photos
  # Based on the breed variable (e.g., "bulldog")
`;

// Use useLazyQuery to fetch dog photos on demand
const [getDog, { loading, error, data }] = useLazyQuery(GET_DOG_PHOTO); // Typo correction
```

---

## Setting a fetch policy

By default, the `useQuery` hook checks the Apollo Client cache to see if all the data you requested is already available locally.You can specify a different fetch policy for a given query. To do so, include the `fetchPolicy` option in your call to `useQuery`:

```js
const { loading, error, data } = useQuery(GET_DOGS, {
  fetchPolicy: "network-only", // Doesn't check cache before making a network request
});
```

`fetchPolicy` is used for the query's first execution, and `nextFetchPolicy` is used to determine how the query responds to future cache updates:

```js
const { loading, error, data } = useQuery(GET_DOGS, {
  fetchPolicy: "network-only", // Used for first execution
  nextFetchPolicy: "cache-first", // Used for subsequent executions
});
```

To know all [Supported fetch policies](https://www.apollographql.com/docs/react/data/queries#supported-fetch-policies)

To know all [`useQuery` API](https://www.apollographql.com/docs/react/data/queries#options)

To know all [Result](https://www.apollographql.com/docs/react/data/queries#result)
