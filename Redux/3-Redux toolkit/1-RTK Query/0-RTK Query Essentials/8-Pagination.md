# Pagination

RTK Query does not include any built-in pagination behavior. However, RTK Query does make it straightforward to integrate with a standard index-based pagination API. This is the most common form of pagination that you'll need to implement.

**Setup an endpoint to accept a page `arg`**

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

export const api = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: "/" }),
  endpoints: (builder) => ({
    listPosts: builder.query({
      query: (page = 1) => `posts?page=${page}`,
    }),
  }),
});

export const { useListPostsQuery } = api;
```
