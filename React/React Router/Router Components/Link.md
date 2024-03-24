# Link

`Link` used to navigate between the routes.To tell Link what path to take the user to when clicked, you pass it a to prop.

## Props

- `state`:The `state` property can be used to set a stateful value for the new location which is stored inside history state. This value can subsequently be accessed via [`useLocation()`](../Router%20Hooks/useLocation.md),for example :

```jsx

<Link to="/onboarding/profile" state={{ from: "occupation" }}>
  Next Step
</Link>

// ------------------------------------------------

import { useLocation } from 'react-router-dom'

function Profile () {
  const location = useLocation()
  const { from } = location.state

  return (
    ...
  )
}
```

### Syntax

```jsx
<nav>
  <Link to="/">Home</Link>
  <Link to="/about">About</Link>
  <Link to="/settings">Settings</Link>
</nav>
```
