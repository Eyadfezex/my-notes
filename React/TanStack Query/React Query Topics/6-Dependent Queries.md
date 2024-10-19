# Dependent Queries

Dependent queries are executed in sequence, where the execution of a query depends on the completion of a preceding query. TanStack Query offers two main approaches to handle dependent queries:

## Types of Dependent Queries

### 1. useQuery Dependent Query

Dependent (or serial) queries can be easily managed using the `enabled` option in the `useQuery` hook. This option allows a query to run only when certain conditions are met, such as the completion of a previous query.

**Example:**

```tsx
// Fetch the user data using the provided email
const { data: user } = useQuery({
  queryKey: ["user", email], // Unique key for the query
  queryFn: getUserByEmail, // Function to fetch user data
});

// Extract the user ID from the fetched user data
const userId = user?.id;

// Fetch the user's projects only if userId exists
const {
  status,
  fetchStatus,
  data: projects,
} = useQuery({
  queryKey: ["projects", userId], // Unique key for the projects query
  queryFn: getProjectsByUser, // Function to fetch projects by user ID
  enabled: !!userId, // Enable this query only when userId is defined
});
```

### 2. useQueries Dependent Query

The `useQueries` hook can also handle dynamic parallel queries with dependencies. This is useful when multiple queries need to depend on the result of a previous query.

**Example:**

```tsx
// Fetch the user IDs
const { data: userIds } = useQuery({
  queryKey: ["users"], // Unique key for the users query
  queryFn: getUsersData, // Function to fetch all users
  select: (users) => users.map((user) => user.id), // Extract user IDs from the fetched data
});

// Fetch messages for each user ID
const usersMessages = useQueries({
  queries: userIds // Check if userIds is defined
    ? userIds.map((id) => ({
        queryKey: ["messages", id], // Unique key for each user's messages query
        queryFn: () => getMessagesByUsers(id), // Function to fetch messages by user ID
      }))
    : [], // If userIds is undefined, return an empty array
});
```
