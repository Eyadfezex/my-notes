# Socket.IO Client Initialization

Socket.IO enables low-latency, bidirectional, and event-based communication between a client and a server. Below are the steps and details for initializing a Socket.IO client.

## 1. From the Same Domain

If your frontend is served from the same domain as your server, you can initialize the client without specifying the server URL:

```javascript
const socket = io();
```

- The server URL is inferred from `window.location`.

---

## 2. From a Different Domain

If your frontend and backend are on different domains, specify the server URL explicitly:

```javascript
const socket = io("https://server-domain.com");
```

- Ensure that **Cross-Origin Resource Sharing (CORS)** is enabled on the server to allow connections from different origins.

---

## 3. Connecting to a Custom Namespace

By default, the client connects to the main namespace. To connect to a custom namespace:

### a) Same Origin

```javascript
const socket = io("/admin");
```

### b) Cross-Origin

```javascript
const socket = io("https://server-domain.com/admin");
```

- **Namespaces** allow for better separation of concerns within your application.

---

## 4. Importing the `io` Object

Depending on your setup, import the `io` object using one of the following methods:

### a) Using `<script>` Tag

```html
<script src="/socket.io/socket.io.js"></script>
```

### b) Using ESM Import (CDN)

```javascript
import { io } from "https://cdn.socket.io/4.8.1/socket.io.esm.min.js";
```

### c) Using NPM (CommonJS)

```javascript
const { io } = require("socket.io-client");
```

### d) Using NPM (ES Modules or TypeScript)

```javascript
import { io } from "socket.io-client";
```

---

## 5. Configuring Client Options

Socket.IO provides a variety of options to customize client behavior. For example:

```javascript
const socket = io("https://server-domain.com", {
  reconnectionDelayMax: 10000,
  auth: { token: "123" },
  query: { userId: "abc" },
});
```

- For a comprehensive list of options, refer to the [official documentation](https://socket.io/docs/v4/client-initialization/).

---

## 6. TypeScript Support

For TypeScript users, you can provide type hints for events to improve the development experience. Example:

```typescript
const socket = io("https://server-domain.com");

socket.on("message", (data: string) => {
  console.log(data);
});
```

---

### **Important Notes**

- Always ensure that the **server and client configurations** are compatible to establish a successful connection.
- Use appropriate CORS settings if working across different origins.

For more details, visit the [Socket.IO Documentation](https://socket.io/docs/v4/client-initialization/).
