# What is SSE?

**SSE (Server-Sent Events)** is a standard that allows servers to push real-time updates to web pages over a single, long-lived HTTP connection. Unlike traditional web requests where the client must keep asking "Is there new data yet?", the server simply sends data whenever a new event occurs.

## How it Works

1. **The Handshake:** The client (browser) sends a standard GET request to the server.
2. **The Agreement:** The server responds with a specific header: `Content-Type: text/event-stream`. This tells the browser, "Don't close this connection; I'm going to keep sending data."
3. **The Stream:** The connection remains open. Whenever the server has news, it sends a block of text starting with `data:`.

---

## Pros and Cons of SSE

### The Pros (Advantages)

- **Simple Implementation:** Since it uses standard HTTP, you don’t need a complex handshake or a different protocol (unlike WebSockets).
- **Automatic Reconnection:** Browsers are designed to automatically reconnect to the server if the connection is lost. It even tracks the "Last-Event-ID" so the server knows where to pick up.
- **Battery & Resource Efficient:** It is much lighter on mobile devices and browsers than "polling" (where the client asks for data every few seconds).
- **Firewall Friendly:** Because it's just regular HTTP traffic, it usually passes through corporate firewalls and proxies without needing special configuration.

### The Cons (Limitations)

- **One-Way Only:** The client cannot send data back to the server through the same connection. To send data, the client must open a _new_ separate HTTP request (like a POST or PUT).
- **Maximum Connection Limit:** When not using HTTP/2, browsers have a strict limit on the number of open connections to a single domain (usually **6**). This can be a bottleneck if a user has many tabs open.
- **Text-Only Data:** SSE is designed to send UTF-8 text. While you can send JSON, it isn't natively built for sending binary data (like images or raw files).

---

## Key Characteristics

- **Unidirectional:** Data flows one way—from the **server to the client**. This makes it simpler and more efficient than WebSockets if you don't need the client to talk back constantly.
- **Automatic Reconnection:** If the connection drops, the browser is built to automatically try to reconnect.
- **Lightweight:** It runs over standard HTTP, meaning it doesn't require special protocols or complex server configurations.
