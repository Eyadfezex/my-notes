# createPortal API

The `createPortal` API allows you to render React children into a different part of the DOM outside the current component hierarchy.

---

## Syntax

```jsx
import { createPortal } from "react-dom";

createPortal(children, domNode, key?)
```

---

## Parameters

- **`children`**: The React nodes you want to render in the portal.
- **`domNode`**: The DOM element where the children will be rendered.
- **`key?`**: An optional key to uniquely identify the portal. Useful for optimization.

---

## Usage Example

Here's how you can use `createPortal` to render a child into a different part of the DOM:

```jsx
import React from "react";
import { createPortal } from "react-dom";

function PortalExample() {
  return (
    <div>
      <p>This child is rendered within the parent div.</p>
      {createPortal(
        <p>This child is rendered directly in the document body.</p>,
        document.body
      )}
    </div>
  );
}

export default PortalExample;
```

---

## When to Use `createPortal`

`createPortal` is commonly used in scenarios where rendering outside the React component tree is necessary. Examples include:

- Modals
- Tooltips
- Popovers
- Notifications

By leveraging `createPortal`, these UI elements can be placed outside the main DOM hierarchy, making them easier to style and manage.

---

## Notes

1. **Event Bubbling**: Events triggered inside a portal bubble up through the React component tree as if they were within the parent component. React ensures consistent event delegation.
2. **Styling**: Ensure that the styles for portal children are accessible in the context of their new DOM location.

---

For more details, refer to the [React documentation on portals](https://reactjs.org/docs/portals.html).
