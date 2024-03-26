# Store

The current Redux application state lives in an object called the store .

The store is created by passing in a reducer, and has a method called `getState` that returns the current state value:

```js
import { configureStore } from "@reduxjs/toolkit";

const store = configureStore({ reducer: counterReducer });

console.log(store.getState());
// {value: 0}
```
