# Actions

An action in Redux is a simple JavaScript object with a `type` field, representing an event in the application. The `type` field usually follows the convention "feature/eventName", indicating the feature or category, and the specific event. Additional information can be included in a field named `payload`,for example:

```js
const addTodoAction = {
  type: "todos/todoAdded",
  payload: "Buy milk",
};
```

Actions are executed via the `dispatch()` method, which forwards the action to the store:
![action](../../../img/redux_action.png)

## Action Creators

An **action creator** is a function that creates and returns an action object. We typically use these so we don't have to write the action object by hand every time:

```js
const addTodo = (text) => {
  return {
    type: "todos/todoAdded",
    payload: text,
  };
};
```
