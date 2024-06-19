# Fetching with Suspense

The `useSuspenseQuery` hook initiates a network request and causes the component calling it to suspend while the request is made.
**For example:**

```tsx
// Define the GraphQL query document with a comment explaining cache key behavior
const GET_DOG_QUERY: TypedDocumentNode<Data, Variables> = gql`
  query GetDog($id: String) {
    dog(id: $id) {
      id
      name
      breed
    }
  }
`;

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Dog id="3" />
    </Suspense>
  );
}

function Dog({ id }: DogProps) {
  // Use useSuspenseQuery hook with comments on variables and data access
  const { data } = useSuspenseQuery(GET_DOG_QUERY, {
    variables: { id }, // Pass the id prop as a variable
  });

  return <>Name: {data.dog.name}</>;
}
```

---

## Updating state without suspending

To Updating state without suspending, it's done with Something like `startTransition` (react API) or `useStartTransition` (react hook) to show bending feedback on the screen.

[to know more about `startTransition`](../../../../React/APIs/startTransition.md)
[to know more about `useStartTransition`](../../../../React/Hooks/useTransition.md)

---

## Rendering partial data

To render a cached partial data without suspending use `returnPartialData` option, like this:

```tsx
const { data } = useSuspenseQuery(GET_DOG_QUERY, {
  variables: { id },
  returnPartialData: true,
});
```

---

## Error handling

By default, both network errors and GraphQL errors thrown by `useSuspenseQuery`.

```ts
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return this.props.children;
    }

    return this.props.children;
  }
}
```

When the query inside of the Dog component returns a GraphQL error or a network error, `useSuspenseQuery` throws the error and the nearest error boundary renders its fallback component.

like this:

```ts
const App = () => {

  return (
    <ErrorBoundary fallback={<div>Something went wrong</div>}>
      <Suspense fallback={<div>Loading...</div>}>
        <Dog id={selectedDog} />
      </Suspense>
    </ErrorBoundary>;
  )
};
```

When the useSuspenseQuery hook inside the Dog component throw an error, the `ErrorBoundary` catches it and display the `fallback`.

---

## Avoiding request waterfalls

A tree of components that all use `useSuspenseQuery` can cause a "waterfall", where each call to `useSuspenseQuery` depends on the previous to complete before it can start fetching. This can be avoided by fetching with [`useBackgroundQuery`](../hooks/3-useBackgroundQuery.md) and reading the data with `useReadQuery`.

**For Example:**

```tsx
// Import necessary Apollo Client hooks (assumed)
import {
  useBackgroundQuery,
  useSuspenseQuery,
  useReadQuery,
} from "@apollo/client";

// Assuming GET_BREEDS_QUERY and GET_DOG_QUERY are defined elsewhere

function App() {
  // Initiate the request for dog breeds in the background using useBackgroundQuery
  const [queryRef] = useBackgroundQuery(GET_BREEDS_QUERY);

  return (
    <Suspense fallback={<div>Loading...</div>}>
      {/* Pass the query reference to Dog component to access breeds data */}
      <Dog id="3" queryRef={queryRef} />
    </Suspense>
  );
}

function Dog({ id, queryRef }: DogProps) {
  // Fetch data for a specific dog (ID provided) using useSuspenseQuery
  const { data } = useSuspenseQuery(GET_DOG_QUERY, {
    variables: { id },
  });

  return (
    <>
      Name: {data.dog.name}
      {/* Suspend rendering of Breeds until breeds data is available */}
      <Suspense fallback={<div>Loading breeds...</div>}>
        <Breeds queryRef={queryRef} />
      </Suspense>
    </>
  );
}

interface BreedsProps {
  queryRef: QueryRef<BreedData>;
}

function Breeds({ queryRef }: BreedsProps) {
  // Use useReadQuery to access breed data from the previously initiated background request
  const { data } = useReadQuery(queryRef);

  return data.breeds.map(({ characteristics }) =>
    characteristics.map((characteristic) => (
      <div key={characteristic}>{characteristic}</div>
    ))
  );
}
```

- App initiates `GET_BREEDS_QUERY` in the background (no blocking).
- Dog fetches specific dog data (`GET_DOG_QUERY`) and suspends.
- Breeds uses `queryRef` from Dog to access pre-fetched breeds data (from App's background request).
- No additional network call or suspension, Breeds renders breeds immediately.

---

## Fetching in response to user interaction

The `useSuspenseQuery` & `useBackgroundQuery` hooks don't work with user interactions.

The [`useLoadableQuery`](../hooks/4-useLoadableQuery.md) hook initiates a network request in response to user interaction.

[To know how to use it](../hooks/4-useLoadableQuery.md)

---

## How to make a preload query with Apollo client

In Apollo Client `createQueryPreloader` is a function that helps with pre-fetching data outside of React components. It allows you to initiate a GraphQL query **before** it's actually needed for rendering.

**How it's works:**

- Takes an `ApolloClient` instance as an argument.
- Returns a function (`preloadQuery`) that, when called with a query document, initiates the network request to fetch data.
- **Does not** render any UI or handle data access directly.

**For Example:**

```tsx
import { ApolloClient, InMemoryCache, gql } from "@apollo/client";
import { createQueryPreloader } from "@apollo/client";

const client = new ApolloClient({
  cache: new InMemoryCache(),
  uri: "https://your-graphql-endpoint.com",
});

const preloadUserQuery = createQueryPreloader(client);

// Pre-fetch user data before rendering the Profile component
preloadUserQuery(
  gql`
    query User($id: ID!) {
      user(id: $id) {
        id
        name
      }
    }
  `,
  { variables: { id: 123 } }
);

// In your Profile component (can be rendered later)
function Profile() {
  const { data } = useQuery(USER_QUERY, { variables: { id: 123 } });

  // Data should be available immediately because it was pre-fetched
  return (
    <div>
      <h2>{data.user.name}</h2>
    </div>
  );
}
```

---

## Refetching and pagination
