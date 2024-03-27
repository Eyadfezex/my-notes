# state management

**Inside a Single Component:**

- **Imagine a counter app where you can click a button to increase the count.**
- **React lets you manage this state directly within the component:**
  - The counter value is stored in a variable called `counter`.
  - A function called `increment` updates the counter when the button is clicked.
  - The button's `onClick` property calls `increment` when pressed.
  - The component's UI (the `<div>` and `<button>`) displays the current counter value.

**Managing Shared State Across Components:**

- **Now, envision a more complex app with multiple components needing to access and update the same counter.**
- **Redux steps in to provide a centralized store for shared state:**
  - The counter value is now stored in the Redux [store](../thinking%20in%20redux/Glossary.md), accessible to any component.
  - Components dispatch "actions" (like "INCREMENT_COUNTER") to signal state changes.
  - A "reducer" function receives actions and updates the store accordingly.
  - Components can subscribe to store changes and re-render when the counter updates.

**Benefits of Redux for Shared State:**

- **Centralized state:** Keeps data organized and consistent across the app.
- **Predictable updates:** Ensures changes happen in a controlled, predictable way.
- **Debugging tools:** Enables logging actions, time-travel debugging, and easier error tracking.
- **Ideal for large, complex apps:** Helps manage state effectively and maintain code clarity.
