# useSelector

`useSelector` from React Redux connects React components to the Redux store, allowing them to extract specific parts of the state. It's a hook that takes a selector function, defining which state to access. When the selected state changes, the component automatically re-renders. Here's a concise version of your example:

```javascript
import React from "react";
import { useSelector } from "react-redux";

const MyComponent = () => {
  // Extracting 'counter' and 'user' from the Redux store state
  const { counter, user } = useSelector((state) => ({
    counter: state.counter,
    user: state.user,
  }));

  return (
    <div>
      <p>Counter: {counter}</p>
      <p>User: {user.name}</p>
    </div>
  );
};

export default MyComponent;
```
