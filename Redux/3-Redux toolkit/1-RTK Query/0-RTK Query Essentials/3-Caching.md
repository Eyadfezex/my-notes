# Caching Strategies with RTK Query

Caching is an essential feature of RTK Query that improves performance by reusing previously fetched data.

## Cache Invalidation and Cache Entry Lifecycle

RTK Query provides mechanisms to invalidate cached data to ensure the UI displays the most current information. You can specify conditions under which the cache should be invalidated:

```ts
export const apiSlice = createApi({
  // ...other slice properties
  endpoints: (builder) => ({
    getPosts: builder.query<Post[], void>({
      query: () => "posts",
      providesTags: ["Post"],
    }),
    addPost: builder.mutation<Post, Partial<Post>>({
      query: (newPost) => ({
        url: "posts",
        method: "POST",
        body: newPost,
      }),
      invalidatesTags: ["Post"],
    }),
  }),
});
```
