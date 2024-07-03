# React Server Components

React Server Components represent a new paradigm in React development. They run on the web server during page requests, allowing you to access your data layer without the need to build an API. This enables server-side rendering of your React components, sending the rendered result to the client side for display.

## Key Features

- **Server-Side Data Access:** Access your data layer directly from the server, avoiding the need to create separate APIs.
- **Server-Side Rendering:** Render components on the server and send the result to the client, improving performance and reducing initial load times.

## Example

```jsx
import db from "./database";

async function Note({ id }) {
  // NOTE: loads *during* render.
  const note = await db.notes.get(id);
  return (
    <div>
      <Author id={note.authorId} />
      <p>{note}</p>
    </div>
  );
}

async function Author({ id }) {
  // NOTE: loads *after* Note,
  // but is fast if data is co-located.
  const author = await db.authors.get(id);
  return <span>By: {author.name}</span>;
}
```

In this example, the `Note` component fetches data from a database during rendering. The `Author` component fetches data after `Note`, but it can be fast if the data is co-located.

The bundler combines the data, rendered Server Components, and dynamic Client Components into a bundle. Optionally, this bundle can be server-side rendered (SSR) to create the initial HTML for the page. When the page loads, the browser does not see the original `Note` and `Author` components; only the rendered output is sent to the client:

```html
<div>
  <span>By: The React Team</span>
  <p>React 19 is...</p>
</div>
```

Server Components can be dynamic by re-fetching them from a server, where they can access the data and render again. This architecture combines the simple “request/response” model of server-centric Multi-Page Apps with the seamless interactivity of client-centric Single-Page Apps, offering the best of both worlds.

## Adding Actions to Server Components

Server Components are not sent to the browser, so they cannot use interactive APIs like `useState`. However, you can compose them with Client Components using the `"use client"` directive.

**Note:** There is no directive for Server Components. A common misunderstanding is that Server Components are denoted by `"use server"`, but there is no such directive. The `"use server"` directive is used for Server Actions.

### For Example

```jsx
// Server Component
import Expandable from "./Expandable";

async function Notes() {
  const notes = await db.notes.getAll();
  return (
    <div>
      {notes.map((note) => (
        <Expandable key={note.id}>
          <p note={note} />
        </Expandable>
      ))}
    </div>
  );
}

// Client Component
("use client");

export default function Expandable({ children }) {
  const [expanded, setExpanded] = useState(false);
  return (
    <div>
      <button onClick={() => setExpanded(!expanded)}>Toggle</button>
      {expanded && children}
    </div>
  );
}
```

In this example, the `Notes` component fetches data on the server, while the `Expandable` component runs on the client. This composition allows you to combine server-side data fetching with client-side interactivity.
