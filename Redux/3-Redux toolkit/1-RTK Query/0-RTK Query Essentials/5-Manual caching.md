# Manual Cache Updates

**Overview:**
there are use cases when manual cache updates are necessary, such as "optimistic" or "pessimistic" updates, or modifying data as part of cache entry lifecycles.

**RTK Query exports thunks for these use cases, attached to `api.utils`:**

- [`updateQueryData`](../1-RTK%20Query%20API/createApi.md): updates an already existing cache entry
- [`upsertQueryData`](../1-RTK%20Query%20API/createApi.md): creates or replaces cache entries

---

## Optimistic Updates

**The core concepts for an optimistic update are:**

- when you start a query or mutation, `onQueryStarted` will be executed
- you manually update the cached data by dispatching `api.util.updateQueryData` within `onQueryStarted`
- **then, in the case that queryFulfilled rejects:**
  - you roll it back via the `.undo` property of the object you got back from the earlier dispatch, OR
  - you invalidate the cache data via `api.util.invalidateTags` to trigger a full re-fetch of the data

**For example:**

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query";

// Create an API slice for managing posts data
const api = createApi({
  // Set a base URL for all API calls
  baseQuery: fetchBaseQuery({ baseUrl: "/" }),

  // Define a cache tag for post-related data
  tagTypes: ["Post"],

  // Define the endpoints for data fetching and mutations
  endpoints: (build) => ({
    // Query endpoint to fetch a specific post by its ID
    getPost: build.query({
      query: (id) => `post/${id}`,
      // Assign the "Post" cache tag to the fetched post data
      providesTags: ["Post"],
    }),

    // Mutation endpoint to update an existing post
    updatePost: build.mutation({
      query: ({ id, ...patch }) => ({
        url: `post/${id}`,
        method: "PATCH",
        body: patch,
      }),
      // Handle optimistic updates
      async onQueryStarted({ id, ...patch }, { dispatch, queryFulfilled }) {
        // Perform an optimistic update in the cache first
        const patchResult = dispatch(
          api.util.updateQueryData("getPost", id, (draft) => {
            // Apply the patch to the cached post data
            Object.assign(draft, patch);
          })
        );

        try {
          // Wait for the server update to complete
          await queryFulfilled;
        } catch (error) {
          // Revert the optimistic update if the server request fails
          patchResult.undo();

          // Alternative approach: invalidate the cache tag for a re-fetch
          // dispatch(api.util.invalidateTags(["Post"]))
        }
      },
    }),
  }),
});
```

---

## Pessimistic Updates

**The core concepts for a pessimistic update are:**

- when you start a query or mutation, `onQueryStarted` will be executed
- you await `queryFulfilled` to resolve to an object containing the transformed response from the server in the data property
- you manually update the cached data by dispatching `api.util.updateQueryData` within `onQueryStarted`, using the data in the response from the server for your draft updates
- you manually create a new cache entry by dispatching `api.util.upsertQueryData` within `onQueryStarted`, using the complete Post object returned by backend.

**For Example:**

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query";

// Create an RTK Query API slice for interacting with posts
const api = createApi({
  // Configure the base query using fetchBaseQuery with a base URL of "/"
  baseQuery: fetchBaseQuery({
    baseUrl: "/",
  }),
  // Define tag type "Post" for data caching related to posts
  tagTypes: ["Post"],
  // Define API endpoints using the build object
  endpoints: (build) => ({
    // Get a post by its ID using a GET request
    getPost: build.query({
      // Build the query URL as `post/${id}`
      query: (id) => `post/${id}`,
      // Provide the "Post" tag to the cache for data retrieved by this query
      providesTags: ["Post"],
    }),
    // Create a new post using a POST request
    createPost: build.mutation({
      // Build the query URL as `post/${id}` with HTTP method set to "POST"
      query: ({ id, ...body }) => ({
        url: `post/${id}`,
        method: "POST",
        body,
      }),
      // Function triggered after the mutation is initiated
      async onQueryStarted({ id }, { dispatch, queryFulfilled }) {
        try {
          // Capture the resolved data (createdPost) from the mutation
          const { data: createdPost } = await queryFulfilled;
          // Update the cache for the "getPost" query with the newly created post
          const patchResult = dispatch(
            api.util.upsertQueryData("getPost", id, createdPost)
          );
        } catch (error) {
          // Handle errors during cache update (optional)
          console.error("Error updating cache:", error);
        }
      },
    }),
  }),
});

export default api;
```
