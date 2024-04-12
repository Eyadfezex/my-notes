# RTK Query: Simplifying Data Fetching in Redux

RTK Query simplifies data fetching in Redux, while TypeScript adds type safety. Together, they offer a robust solution for predictable, type-safe state management in web apps.

## What is RTK Query?

RTK Query, part of Redux Toolkit, streamlines data fetching, caching, and state management. It automatically generates React hooks for your API endpoints, making data fetching and caching efficient.

```typescript
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

interface Post {
  id: number;
  title: string;
}

export const apiSlice = createApi({
  reducerPath: "api",
  baseQuery: fetchBaseQuery({ baseUrl: "/api" }),
  endpoints: (builder) => ({
    getPosts: builder.query<Post[], void>({
      query: () => "posts",
    }),
  }),
});
```

This code sets up an API slice using RTK Query and TypeScript. It defines a single endpoint `getPosts` that fetches data from the '/posts' endpoint. The `Post` interface ensures type safety for the fetched data. Adjust the base URL and endpoint configurations as needed for your API.

## Query Endpoints and TypeScript

Query endpoints are the specific functions within an API slice that define how to fetch data for a particular resource.

### Using `builder.query` to Fetch Data

The `builder.query` method is used to define a query endpoint. It takes a query argument and returns a query function that can be used to fetch data.

```typescript
export const apiSlice = createApi({
  // ...other slice properties
  endpoints: (builder) => ({
    getPostById: builder.query<Post, number>({
      query: (id) => `posts/${id}`,
    }),
  }),
});`
```
