# Automated Re-fetching

In Redux, automated re-fetching means data updates occur automatically based on events or state changes, ensuring data remains current without manual intervention.

- [`Providing`](../1-RTK%20Query%20API/createApi.md) tags: A query can have its cached data provide tags. Doing so determines which 'tag' is attached to the cached data returned by the query.

- [`Invalidating`](../1-RTK%20Query%20API/createApi.md) tags: A mutation can invalidate specific cached data based on the tags. Doing so determines which cached data will be either refetched or removed from the cache.

## Providing cache data

Each individual `query` endpoint can have its cached data provide particular tags. Doing so enables a relationship between cached data from one or more query endpoints and the behaviour of one or more mutation endpoints.
**Example of providing tags to the cache**

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query";

const api = createApi({
  baseQuery: fetchBaseQuery({
    baseUrl: "/",
  }),
  tagTypes: ["Post", "User"],
  endpoints: (build) => ({
    getPosts: build.query({
      query: () => "/posts",
      providesTags: ["Post"],
    }),
    getUsers: build.query({
      query: () => "/users",
      providesTags: ["User"],
    }),
    addPost: build.mutation({
      query: (body) => ({
        url: "posts",
        method: "POST",
        body,
      }),
    }),
  }),
});
```

## Invalidating cache data

Each individual mutation endpoint can `invalidate` particular tags for existing cached data. Doing so enables a relationship between cached data from one or more query endpoints and the behavior of one or more mutation endpoints.
**Example of invalidating tags in the cache**

```js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query";

const api = createApi({
  baseQuery: fetchBaseQuery({
    baseUrl: "/",
  }),
  tagTypes: ["Post", "User"],
  endpoints: (build) => ({
    getPosts: build.query({
      query: () => "/posts",
      providesTags: (result, error, arg) =>
        result
          ? [...result.map(({ id }) => ({ type: "Post", id })), "Post"]
          : ["Post"],
    }),
    getUsers: build.query({
      query: () => "/users",
      providesTags: ["User"],
    }),
    addPost: build.mutation({
      query: (body) => ({
        url: "post",
        method: "POST",
        body,
      }),
      invalidatesTags: ["Post"],
    }),
  }),
});
```

---

## General tag

`['Post'] / [{ type: 'Post' }]`

Will `invalidate` any `provided` tag with the matching type, including general and specific tags.

## Specific tag

`[{ type: 'Post', id: 1 }]`

Will `invalidate` any `provided` tag with both the matching type, and matching id. Will not cause a `general` tag to be invalidated directly, but might invalidate data for an endpoint that provides a `general` tag if it also provides a matching `specific` tag.

The matrix below shows examples of which invalidated tags will affect and invalidate which provided tags:

| Tag Type        | General tag A                   | General tag B                   | Specific tag A1             | Specific Tag A2                  | Specific Tag B1             | Specific Tag B2             |
| --------------- | ------------------------------- | ------------------------------- | --------------------------- | -------------------------------- | --------------------------- | --------------------------- |
| **Provided**    | `['Post']`                      | `['User']`                      | `[{ type: 'Post', id: 1 }]` | `[{ type: 'Post', id: 'LIST' }]` | `[{ type: 'User', id: 1 }]` | `[{ type: 'User', id: 2 }]` |
| **Invalidated** | `['Post'] / [{ type: 'Post' }]` | `['User'] / [{ type: 'User' }]` | `[{ type: 'Post', id: 1 }]` | `[{ type: 'Post', id: 'LIST' }]` | `[{ type: 'User', id: 1 }]` | `[{ type: 'User', id: 2 }]` |

---

## common provides / invalidates usage

The code written to `provide` & `invalidate` tags for a given API slice will be dependent on multiple factors, including:

- The shape of the data returned by your backend
- Which tags you expect a given query endpoint to provide
- Which tags you expect a given mutation endpoint to invalidate
- The extent that you wish to use the invalidation feature for

**for example:**

```js
function providesList(resultsWithIds, tagType) {
  return resultsWithIds
    ? [
        { type: tagType, id: "LIST" },
        ...resultsWithIds.map(({ id }) => ({ type: tagType, id })),
      ]
    : [{ type: tagType, id: "LIST" }];
}
```
