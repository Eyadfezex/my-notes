# `createApi`

`createApi` is a pivotal feature of [RTK Query](../../../2-Redux%20Essentials/8-RTK%20Query%20Basics.md), empowering developers to craft endpoints for fetching data from APIs and other asynchronous sources. It generates an "API slice" structure imbued with Redux logic and optional React hooks, simplifying data fetching and caching.

## Parameters

- `baseQuery`: Configures network requests in RTK Query, defining default behaviors such as headers and error handling.

- `endpoints`: Defines specific API endpoints, encompassing fetching logic, URLs, query parameters, transformations, and caching mechanisms.

- `tagTypes`: Manages cached data to facilitate efficient re-fetching, grouping and organizing data based on entity types or query statuses.

- `reducerPath`: Determines the key under which the generated reducer is stored in the Redux store, facilitating organization and enabling multiple API slices within the same store without conflicts.

- `refetchOnMountOrArgChange`:Defaults to `false`. This setting allows you to control whether if a cached result is already available RTK Query will only serve a cached result, or if it should `refetch` when set to `true` or if an adequate amount of time has passed since the last successful query result.

- `refetchOnReconnect`: Defaults to `false`. This setting allows you to control whether RTK Query will try to refetch all subscribed queries after regaining a network connection.

## Anatomy of an Endpoint

- `query`: Embedded within an endpoint definition, this function dictates the logic for fetching data from the backend API, encompassing parameters, transformations, and other requisites for data retrieval.

- `invalidatesTags`: An advanced feature enabling developers to specify cache tags to invalidate upon executing a particular query, ensuring that relevant cached data is refreshed or cleared, thereby maintaining data coherence across the application.

- `onQueryStarted`: Is a callback function triggered at the start of each query or mutation. It's provided with a lifecycle API object, offering hooks like `queryFulfilled` to execute code during different phases of a query/mutation's lifecycle, from initiation to completion or failure and it's used in **Optimistic Updates and Caching Logic**.

-`transformResponse`:A function to manipulate the data returned by a query or mutation.

- `keepUnusedDataFor`: keepUnusedDataFor is an option used in RTK Query to control the caching behavior of fetched data. It specifies the duration (in seconds) for which RTK Query will retain data in the cache after the last component unsubscribes from that dat

- `onCacheEntryAdded`: This function is triggered when a new cache entry is added, providing a lifecycle object with properties like `cacheDataLoaded` and `cacheDataRemoved` for managing cache lifecycle actions.

  - **Common Use Case: Setting Up Long-Running Operations**

    - A primary use case for onCacheEntryAdded is to establish long-running operations (like WebSocket connections) that keep the cached data up-to-date.

---

**Example Usage for `createApi` with `fetchBaseQuery` to create a API slice**

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

const api = createApi({
  reducerPath: "api",
  baseQuery: fetchBaseQuery({ baseUrl: "/api" }),
  endpoints: (builder) => ({
    // Define endpoint for fetching posts
    getPosts: builder.query({
      query: () => "posts",
      // Define invalidation rules for tags
      invalidatesTags: ["Posts"],
    }),
    // Define endpoint for fetching users
    getUsers: builder.query({
      query: () => "users",
      invalidatesTags: ["Users"],
    }),
  }),
  tagTypes: ["Posts", "Users"],
});

export const { useGetPostsQuery, useGetUsersQuery } = api;
```

In this example, `createApi` is utilized to establish an API slice with a base URL of '/api'. Two endpoints, `getPosts` and `getUsers`, are defined, each specifying a query function and invalidating their respective cache tags upon execution. The generated hooks `useGetPostsQuery` and `useGetUsersQuery` can be leveraged to retrieve posts and users data, respectively.
