# Writing Async Logic with Thunks

Thunks in Redux allow handling asynchronous logic within actions. They consist of an inner function receiving `dispatch` and `getState`, and an outer creator function. Redux Toolkit simplifies their use, automatically configuring the `redux-thunk` middleware in `configureStore`.

Example of a thunk:

```javascript
export const incrementAsync = (amount) => (dispatch) => {
  setTimeout(() => {
    dispatch(incrementByAmount(amount));
  }, 1000);
};
```

To use thunks:

```javascript
store.dispatch(incrementAsync(5));
```
