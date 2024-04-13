# Error Handling

**Overview**
If your query or mutation happens to throw an error when using [fetchBaseQuery](../1-RTK%20Query%20API/fetchBaseQuery.md), it will be returned in the `error` property of the respective hook. The component will re-render when that occurs, and you can show appropriate UI based on the error data if desired.

**Error Display Examples:**

```js
//Query Error

function PostsList() {
  const { data, error } = useGetPostsQuery();

  return (
    <div>
      {error.status} {JSON.stringify(error.data)}
    </div>
  );
}
//Mutation Error

function AddPost() {
  const [addPost, { error }] = useAddPostMutation();

  return (
    <div>
      {error.status} {JSON.stringify(error.data)}
    </div>
  );
}
```

---

## Errors with a custom baseQuery

Whether a response is returned as `data` or `error` is dictated by the `baseQuery` provided.

---

## Handling errors at a macro level
