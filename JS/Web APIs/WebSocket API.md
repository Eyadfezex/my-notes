# WebSocket API

The WebSocket API enables **interactive, bidirectional communication** between a user's browser and a server. This allows real-time data exchange without the overhead of continuous HTTP polling.

## Key Interfaces

- **`WebSocket`**:  
  The primary interface for creating WebSocket connections, sending/receiving data, and handling connection events.

- **`WebSocketStream`**:  
  A promise-based, experimental alternative that integrates with the Streams API to manage backpressure for efficient data flow. Note that this interface is **non-standard** and has **limited browser support**.

## Establishing a Connection

To initiate a WebSocket connection, instantiate the `WebSocket` class with the server URL:

```javascript
const socket = new WebSocket("ws://example.com");
```

This automatically begins the connection process.

## Sending and Receiving Data

### Sending Data

Transmit data to the server using the `send()` method:

```javascript
socket.send("Hello, Server!");
```

### Receiving Data

Handle incoming messages by assigning a function to the `onmessage` event handler:

```javascript
socket.onmessage = (event) => {
  console.log("Message from server:", event.data);
};
```

## Monitoring Connection Events

You can monitor the WebSocket's lifecycle with event handlers:

- **Connection Opened**: Triggered when the connection is successfully established.

  ```javascript
  socket.onopen = () => {
    console.log("Connection opened.");
  };
  ```

- **Connection Closed**: Triggered when the connection is closed (intentionally or otherwise).

  ```javascript
  socket.onclose = (event) => {
    console.log("Connection closed:", event.code, event.reason);
  };
  ```

- **Error Occurred**: Triggered when an error occurs with the connection.

  ```javascript
  socket.onerror = (event) => {
    console.error("WebSocket error:", event);
  };
  ```

## Closing the Connection

To terminate the WebSocket connection, use the `close()` method. Optionally, provide a status code and a reason for the closure:

```javascript
socket.close(1000, "Normal closure");
```

## Security Considerations

- Use **`wss://`** (WebSocket Secure) instead of `ws://` to ensure encrypted communication when working over HTTPS.
- Always validate and sanitize incoming data to prevent security risks such as injection attacks.

## Browser Compatibility

The `WebSocket` interface is widely supported in all modern browsers. However, the `WebSocketStream` interface is still experimental and should only be used in environments where its support is confirmed.

## Simplifying WebSocket Development

For easier and more feature-rich WebSocket handling, consider libraries like **Socket.IO**, which abstracts WebSocket intricacies and offers robust fallback mechanisms.

## Further Reading

For detailed documentation, visit the [MDN Web Docs on WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API).
