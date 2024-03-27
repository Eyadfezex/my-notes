# Redux Store: The Central Hub

The Redux store is the heart of your Redux application. It acts as a single source of truth for the entire application state, ensuring consistency and predictability.

**Creating the Store:**

You create a store by providing it with a root reducer function using the `configureStore` function from the `@reduxjs/toolkit` library (or `createStore` from Redux itself). The root reducer combines all your reducers into a single function that manages the entire state tree.

**Accessing the State:**

The store provides a `getState` method that allows you to retrieve the current state value at any point in your application. This is handy for debugging or logging purposes.

Here's an example of creating a store and accessing the initial state:

```javascript
import { configureStore } from "@reduxjs/toolkit";

const counterReducer = (state = { value: 0 }, action) => {
  // ... reducer logic
};

const store = configureStore({ reducer: counterReducer });

console.log(store.getState()); // {value: 0}
```

By keeping your application state centralized in the Redux store, you gain better control and maintainability over your application's data.
