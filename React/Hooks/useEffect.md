## useEffect Hook

- useEffect is a React Hook that lets you [synchronize a component with an external system.](https://react.dev/learn/synchronizing-with-effects)

```jsx
 useEffect(setup, dependencies?)
```

## Parameters

- `setup`: The function with your Effect’s logic.
- **optional** `dependencies`: The list of all reactive values referenced inside of the setup code.

## Return

`useEffect` returns `undefined`.

## Syntax

```jsx
import { useEffect } from "react";
import { createConnection } from "./chat.js";

function ChatRoom({ roomId }) {
  const [serverUrl, setServerUrl] = useState("https://localhost:1234");

  useEffect(() => {
    const connection = createConnection(serverUrl, roomId);
    connection.connect();
    return () => {
      connection.disconnect();
    };
  }, [serverUrl, roomId]);
  // ...
}
```

[`For more info`](https://react.dev/reference/react/useEffect)
