# Intro to Apollo Client

Apollo Client is a comprehensive state management library for JavaScript. It enables you to manage both local and remote data with GraphQL. Use it to fetch, cache, and modify application data, all while automatically updating your UI.

- **Core features:**
  - Declarative data fetching
  - Normalized request and response caching
  - Designed for modern React

## Why Apollo Client?

- **Declarative data fetching:** Apollo handle request cycle from start to finish include all of error state, loading and caching.
- **Combining local & remote data:** Apollo handle the remote data & local data, apollo have a state management future enable you to use your cached data as the single source of truth for the application.
- **Zero-config caching:** Apollo make all caching futures under the hood with mush configurations, things like automatically overwrite the existing fields of any previously cached data in mutation case, avoid refetching information already contained in our cache,
