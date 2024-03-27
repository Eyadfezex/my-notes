# Redux Glossary

- **State:** Your application's data, all in one place (like a big box).
- **Action:** A message describing an event (like "ADD_TODO").
- **Reducer:** A function that updates the state based on actions (like adding a todo to the box).
- **Dispatch Function:** Tells the store to update the state using an action (like giving instructions to move things around in the box).
- **Action Creator:** A helper function that makes creating actions easier (like a pre-written note for the dispatch function).
- **Async Action:** An action for things that take time (like waiting for data to download before updating the box).
- **Middleware:** Special code that can handle async actions and side effects (like logging or routing) before they affect the state (like a helper to download data and then put it in the box).
- **Store:** Holds the state and provides ways to interact with it (like the box itself, with functions to get things out, put things in, and listen for changes).
- **Store Creator:** Builds a store (like a factory for the box).
- **Store Enhancer:** Adds features to the store creation process (like making the box bigger or adding wheels).
