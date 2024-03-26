# Component State and Forms

In a React + Redux app, it's vital to decide what state belongs in the Redux store versus local component state.

For example, consider the input textbox in `<Counter>`:

```javascript
const [incrementAmount, setIncrementAmount] = useState("2");

// later
return (
  <div className={styles.row}>
    <input
      className={styles.textbox}
      aria-label="Set increment amount"
      value={incrementAmount}
      onChange={(e) => setIncrementAmount(e.target.value)}
    />
    <button
      className={styles.button}
      onClick={() => dispatch(incrementByAmount(Number(incrementAmount) || 0))}
    >
      Add Amount
    </button>
    <button
      className={styles.asyncButton}
      onClick={() => dispatch(incrementAsync(Number(incrementAmount) || 0))}
    >
      Add Async
    </button>
  </div>
);
```

Updating the input's text string in Redux via actions isn't necessary since it's only used within `<Counter>`. Thus, managing this state with `useState` is more suitable.

Similarly, local flags like `isDropdownOpen` should stay within the component if they're specific to it.

Here are guidelines for Redux state:

- Is the data needed elsewhere?
- Is it used to derive other data?
- Is it shared across components?
- Is time-travel debugging needed?
- Do you want to cache it or maintain consistency during hot-reloading UI components?

For form state, it's often better to keep it in local component state and dispatch actions to update the store as needed.

Lastly, notice how thunks like `incrementAsync` from `counterSlice.js` are used in this component. It dispatches actions without worrying about the details.
