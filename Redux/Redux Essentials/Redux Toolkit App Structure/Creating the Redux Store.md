# Creating the Redux Store

To create the Redux store using Redux Toolkit's `configureStore` function, we pass a reducer argument. If our application has multiple features with their own reducers, we include them in an object passed to `configureStore`. Each key in this object defines a corresponding section in the state.

For example:

```javascript
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";

export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

Here, `counterReducer` from `features/counter/counterSlice.js` manages the `state.counter` section.

`configureStore` also integrates useful middleware and enhancers for a better developer experience, including setup for the Redux DevTools Extension.
