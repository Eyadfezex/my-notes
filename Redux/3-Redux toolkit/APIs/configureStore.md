# configureStore

Redux Toolkit's `configureStore` simplifies Redux store creation. It combines reducers, adds middleware (including DevTools in development for debugging), and creates the store. This reduces boilerplate and improves developer experience.

## Parameters

- `reducer`**-(Required)**: The root reducer function for your application,it is an object of slice reducers, like `{users : usersReducer, posts : postsReducer}`.
- `middleware`**-(Optional)**: An array of middleware functions for actions (e.g., Redux Thunk).
- `devTools`**-(Optional, Default: true)** :Enables Redux DevTools Extension for debugging (dev only).
- `preloadedState`**-(Optional)**: By default, a Redux store starts with an empty state object. The `preloadedState` parameter allows you to bypass this and set a specific initial state for your application.
- `enhancers`**-Optional)**: An array of functions to further customize store behavior.

**Example:**

```js
import { configureStore } from "@reduxjs/toolkit";

import rootReducer from "./reducers";

const store = configureStore({ reducer: rootReducer });
// The store now has redux-thunk added and the Redux DevTools Extension is turned on
```
