# Redux: Streamlined Data Flow

Redux enforces a one-way data flow for predictable state management.

**Setup:**

1. Create a Redux store with a root reducer (defines state structure).
2. Store initializes state and UI components connect and subscribe.

**Updates:**

1. Events (user interaction) trigger action dispatches to the store.
2. The store calls reducers based on action type.
3. Reducers update the state immutably (create a new state object).
4. Store notifies subscribed components.
5. Components selectively re-render based on state changes.

This unidirectional flow simplifies debugging and maintenance in complex apps.

Here's what that data flow looks like visually:
![data flow in redux](https://redux.js.org/assets/images/ReduxDataFlowDiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)
