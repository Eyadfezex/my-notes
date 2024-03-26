# Reducers and Immutable Updates

In Redux, mutating the original state within reducers is forbidden as it leads to bugs, hinders understanding of state changes, complicates testing, disrupts time-travel debugging, and violates Redux usage patterns.

Reducers should only create copies of the original state and then modify these copies:

```javascript
// ✅ This is safe, as it creates a copy of the state
return {
  ...state,
  value: 123,
};
```

Redux Toolkit's `createSlice` function simplifies immutable updates by utilizing the Immer library, which tracks mutations using a Proxy-based approach. This enables writing code that appears to mutate data while ensuring immutability, thereby reducing the risk of accidental state mutations and enhancing code readability.

Using `createSlice` or `createReducer` from Redux Toolkit with Immer ensures that mutating logic is handled safely. Attempting mutating logic in reducers without Immer can lead to state mutation bugs.
