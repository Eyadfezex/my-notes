# Integrating RTK Query with the Redux Store

RTK Query is designed to work seamlessly with the Redux store, providing a consistent approach to state management.

## Connecting the API Slice to the Redux Store

To connect your API slice to the Redux store, you need to include the generated reducer in your store configuration:

```ts
import { configureStore } from "@reduxjs/toolkit";
import { apiSlice } from "./apiSlice";

export const store = configureStore({
  reducer: {
    [apiSlice.reducerPath]: apiSlice.reducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(apiSlice.middleware),
});
```
