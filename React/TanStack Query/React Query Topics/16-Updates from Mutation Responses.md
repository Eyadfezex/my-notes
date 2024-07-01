# Updates from Mutation Responses

In React Query, mutations are used to modify data on the server. While the mutation itself handles updating the server, you might also want to update the local cache to reflect those changes immediately. This avoids unnecessary refetches and keeps the UI consistent.

This done in two ways:

1. The `useMutation` hook provides an `onSuccess` callback function that is triggered when the mutation successfully updates the server. Within this callback, you can access the mutation response data and use it to update the cache. Here's an example:

```ts
const { mutate } = useMutation(createTodo);

const handleCreateTodo = async (newTodo) => {
  const { data } = await mutate(newTodo); // Perform mutation
  queryClient.setQueryData(["todos"], (oldTodos) => [...oldTodos, data]); // Update cache with new todo
};
```
