# Redux Application Data Flow

In Redux, the "one-way data flow" process unfolds as follows:

Initial Setup:

1. Create a Redux store using a root reducer.
2. The store initializes its `state` by calling the root reducer.
3. UI components render based on the `initial state` and subscribe for updates.

Updates:

1. An event triggers, like a user clicking a button.
2. App code dispatches an action to the store.
3. The store runs the reducer with previous state and action, saving the result as the new state.
4. Subscribed UI components are notified of the update.
5. Components check if relevant state parts have changed and re-render accordingly.

Here's what that data flow looks like visually:
![data flow in redux](https://redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)
