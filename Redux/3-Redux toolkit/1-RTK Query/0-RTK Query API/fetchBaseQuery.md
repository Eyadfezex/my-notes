# fetchBaseQuery: Simplifying RTK Query Requests

`fetchBaseQuery` is a built-in RTK Query function that streamlines HTTP requests. It wraps the native `fetch` API, offering a lightweight and easy-to-use solution for API interactions.

**Key Benefits:**

- **Concise Code:** Reduces boilerplate compared to manual `fetch` usage.
- **Standardized Configuration:** Provides options for base URL, custom headers (authentication, etc.), and timeouts.
- **Seamless Integration:** Integrates smoothly with RTK Query's data fetching and caching mechanisms.

**Basic Usage:**

```javascript
import { fetchBaseQuery } from "@reduxjs/toolkit/query/react";

const baseQuery = fetchBaseQuery({
  baseUrl: "https://api.example.com",
  prepareHeaders: (headers) => ({
    ...headers,
    "Content-Type": "application/json",
  }),
  timeout: 10000, // Optional timeout in milliseconds
});
```

**Explanation of Parameters:**

- `baseUrl`: The root URL of your API (prepended to all requests).
- `prepareHeaders` (Optional): Customize headers for each request (e.g., authentication tokens).
- `timeout` (Optional): Set a maximum wait time for responses to prevent hanging.

**Leveraging `fetchBaseQuery`:**

Use `baseQuery` as the `baseQuery` property in your [RTK Query API](./createApi.md) definition to make streamlined and efficient HTTP requests.
