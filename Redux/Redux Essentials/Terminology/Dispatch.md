# Dispatch

In Redux, use `store.dispatch()` to update the state by passing an action object. The store's reducer function executes, storing the new state internally, accessible via `getState()`, for example:

```js
store.dispatch({ type: "counter/increment" });

console.log(store.getState());
// {value: 1}
```

`You can think of dispatching actions as "triggering an event"` in the application. Something happened, and we want the store to know about it. Reducers act like event listeners, and when they hear an action they are interested in, they update the state in response.
