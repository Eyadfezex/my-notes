# use API

`use` is a React API that lets you read the value of a resource like a Promise or context.

The `use` API integrates with Suspense and error boundaries for asynchronous operations. When `use` is called with a Promise, the component suspends until the Promise resolves. If wrapped in Suspense, a fallback is shown during suspension. Once resolved, the data is used to render the component. If the Promise rejects, an error boundary's fallback is shown.

**Example:**

```jsx
const value = use(resource);
```

Unlike React Hooks, `use` can be called within loops and conditional statements like if. Like React Hooks, the function that calls `use` must be a Component or Hook.

**Usage:**

- **Reading context with use:** When a context is passed to use, it works similarly to useContext.
