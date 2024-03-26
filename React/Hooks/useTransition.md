# useTransition

`useTransition` is a React Hook that lets you update the state without blocking the UI.

- If you need to start a transition somewhere else (for example, from a data library), call the standalone `startTransition` instead of `useTransition`.
  <br>
- The function you pass to `startTransition` must be synchronous.
  <br>
- A state update marked as a transition will be interrupted by other state updates.
  <br>
- Transition updates can’t be used to control text inputs.
  <br>
- If there are multiple ongoing transitions, React currently batches them together.

```jsx
const [isPending, startTransition] = useTransition();
```

## Returns

`useTransition` returns an array with exactly two items:

1- The `isPending` flag that tells you whether there is a pending transition, it's usually used to add UX feedback.
2- The `startTransition` function that lets you mark a state update as a transition.

## `startTransition` function

The `startTransition` function returned by `useTransition` lets you mark a state update as a transition, for example:

```jsx
function TabContainer() {
  const [isPending, startTransition] = useTransition();
  const [tab, setTab] = useState("about");

  function selectTab(nextTab) {
    startTransition(() => {
      setTab(nextTab);
    });
  }
  // ...
}
```
