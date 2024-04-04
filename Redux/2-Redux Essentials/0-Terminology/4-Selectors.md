# Selectors: State Sleuths

Selectors are functions that act like bloodhounds for your Redux state. They sniff out specific data, keeping component logic clean and reusable. They can also boost performance by optimizing re-calculations.

## Example

```js
const selectCompletedTodos = (state) => {
  return state.todos.filter((todo) => todo.completed);
};

const completedTodos = selectCompletedTodos(store.getState());

console.log(completedTodos); // Array of completed todos
```

In short, selectors simplify state access and make Redux development more efficient.
