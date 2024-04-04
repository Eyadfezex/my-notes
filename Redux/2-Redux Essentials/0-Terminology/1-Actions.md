# Actions in Redux

Actions are the fundamental way to communicate state changes in a Redux application. They are plain JavaScript objects that describe what happened in the application.

## Structure of an Action

An action must have a mandatory `type` property that indicates the type of action being performed. By convention, the `type` property is a string formatted as "feature/eventName" to clearly describe the feature and the specific event that occurred.

Optionally, actions can also include a `payload` property. The `payload` carries any additional information needed to process the action.

Here's an example of an action object:

```javascript
const addTodoAction = {
  type: "todos/todoAdded",
  payload: "Buy milk",
};
```

In this example, the action describes that a todo item has been added ("todos/todoAdded"). The `payload` property carries the content of the new todo item ("Buy milk").

## Dispatching Actions

Actions are sent to the Redux store using the `dispatch()` method. The store then **forwards the action to the reducers**, which will update the application state accordingly.

## Action Creators

To avoid writing action objects by hand every time, we can use action creators. Action creators are functions that return action objects. They typically encapsulate the logic of creating an action and make the code more readable and maintainable.

Here's an example of an action creator for adding a todo:

```javascript
const addTodo = (text) => {
  return {
    type: "todos/todoAdded",
    payload: text,
  };
};
```

The `addTodo` function takes the todo text as input and returns an action object with the appropriate type and payload.

By using action creators, we can improve code readability and maintainability, and ensure that actions are created consistently throughout the application.
