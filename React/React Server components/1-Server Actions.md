# Server Actions in React

Server Actions enable Client Components to call asynchronous functions executed on the server. By using the `"use server"` directive, your framework will automatically create a reference to the server function and pass that reference to the Client Component.

## Defining Server Actions

Server Actions can be created in Server Components and passed as props to Client Components, or they can be imported and used directly in Client Components.

### Example: Server Component

```jsx
// Server Component
import Button from "./Button";

function EmptyNote() {
  async function createNoteAction() {
    // Server Action
    "use server";

    await db.notes.create();
  }

  return <Button onClick={createNoteAction} />;
}
```

In this example, React renders the `EmptyNote` Server Component, creating a reference to the `createNoteAction` function. This reference is then passed to the `Button` Client Component. When the button is clicked, React sends a request to the server to execute the `createNoteAction` function with the provided reference:

### Example: Client Component

```jsx
"use client";

export default function Button({ onClick }) {
  console.log(onClick);
  // Output: {$$typeof: Symbol.for("react.server.reference"), $$id: 'createNoteAction'}
  return <button onClick={onClick}>Create Empty Note</button>;
}
```

## Importing Server Actions in Client Components

Server Actions can also be imported and used directly in Client Components.

### Example

#### Server Component

```jsx
"use server";

export async function createNoteAction() {
  await db.notes.create();
}
```

#### Client Component

```jsx
"use client";
import { createNoteAction } from "./actions";

function EmptyNote() {
  console.log(createNoteAction);
  // Output: {$$typeof: Symbol.for("react.server.reference"), $$id: 'createNoteAction'}
  return <button onClick={createNoteAction}>Create Empty Note</button>;
}
```

## Composing Server Actions with Client Actions

Server Actions can be composed with Client Actions to create more complex interactions.

### Example

#### Server Component

```jsx
"use server";

export async function updateName(name) {
  if (!name) {
    return { error: "Name is required" };
  }
  await db.users.updateName(name);
}
```

#### Client Component

```jsx
"use client";

import { useState, useTransition } from "react";
import { updateName } from "./actions";

function UpdateName() {
  const [name, setName] = useState("");
  const [error, setError] = useState(null);
  const [isPending, startTransition] = useTransition();

  const submitAction = async () => {
    startTransition(async () => {
      const { error } = await updateName(name);
      if (!error) {
        setError(error);
      } else {
        setName("");
      }
    });
  };

  return (
    <div>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button onClick={submitAction}>Update Name</button>
      {error && <p>{error}</p>}
    </div>
  );
}
```

In this example, the `updateName` Server Action is used within a Client Component. The `submitAction` function starts a transition and calls the server action, handling any errors and updating the state accordingly.

---

This enhanced version of your notes includes clearer headings, improved formatting, and additional details to help understand the concepts better.
