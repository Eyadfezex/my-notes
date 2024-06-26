# startTransition

`startTransition` lets you update the state without blocking the UI.

```jsx
startTransition(scope);
```

**Example:**

```jsx
// Tab container component with state management
function TabContainer() {
  // Selected tab state ("about" initially)
  const [tab, setTab] = useState("about");

  // Handles tab selection (updates state with transition)
  function selectTab(nextTab) {
    startTransition(() => setTab(nextTab));
  }
}
```

**parameters:**

- `scope`: A function that updates some state by calling one or more set functions

[To know more About startTransition](https://react.dev/reference/react/startTransition)
