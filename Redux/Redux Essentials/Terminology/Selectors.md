# Selectors

Selectors are functions that know how to extract specific pieces of information from a store state value. As an application grows bigger, this can help avoid repeating logic as different parts of the app need to read the same data:

```js
const selectCounterValue = (state) => state.value;

const currentValue = selectCounterValue(store.getState());
console.log(currentValue);
// 2
```
