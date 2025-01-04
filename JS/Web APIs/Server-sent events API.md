# Server-Sent Events (SSE) API

Server-Sent Events (SSE) provide a mechanism for a server to push real-time updates to a client over a persistent HTTP connection. Unlike traditional HTTP requests, where the client must repeatedly poll the server for updates, SSE allows the server to send data automatically as soon as new information is available. This is particularly useful for applications that require live data feeds, such as notifications, news updates, or real-time analytics.

Once the initial connection is established, the server continuously streams data to the client, typically in the form of plain text messages, structured as `event: data`. This eliminates the need for the client to refresh or make additional requests to retrieve new information.

## Key Features of SSE

- **One-way communication**: Data flows from the server to the client, making SSE ideal for real-time notifications, live feeds, and other unidirectional data streaming use cases.
- **Automatic reconnection**: If the connection is lost, the browser will automatically attempt to reconnect to the server, ensuring uninterrupted data flow with minimal intervention.
- **Text-based format**: SSE messages are transmitted in a simple text format, making them easy to parse and handle on the client side.
- **Efficient**: Compared to polling techniques, SSE is more efficient as it maintains a single open connection and only sends updates when necessary, reducing network overhead.

## Use Cases

- **Push Notifications**: SSE can be used to send real-time notifications, such as alerts for new messages, social media activity, or breaking news.
- **Live Data Streams**: SSE is ideal for displaying frequently updated information like stock market data, sports scores, or weather reports.
- **Collaborative Applications**: In applications that require synchronization across multiple users, such as collaborative text editors or whiteboards, SSE ensures that updates are pushed to all users in real-time.

**Note**: SSE provides one-way communication. For scenarios requiring bi-directional communication (e.g., chat applications), WebSockets might be a better choice.

### Example: Front-End Code to Receive SSE Data

The following JavaScript code demonstrates how a front-end developer can receive and handle real-time data from a server using the `EventSource` API:

```javascript
// Create a new EventSource instance that connects to the SSE endpoint on the server
const eventSource = new EventSource("/sse-endpoint");

// Listen for messages from the server
eventSource.onmessage = function (event) {
  // Parse the received data
  const data = JSON.parse(event.data);

  // Handle the data (e.g., update the UI)
  console.log("New message from server:", data);
  displayMessage(data);
};

// Handle any errors that occur during the connection
eventSource.onerror = function (error) {
  console.error("Error with SSE connection:", error);
  eventSource.close(); // Close the connection in case of an error
};

// Function to update the UI with the new message
function displayMessage(data) {
  const messageContainer = document.getElementById("messages");
  const messageElement = document.createElement("div");
  messageElement.textContent = `New update: ${data.message}`;
  messageContainer.appendChild(messageElement);
}
```

### Explanation

1. **Front-End**:

   - The `EventSource` API is used to create a persistent connection to the SSE endpoint (`/sse-endpoint`).
   - The browser automatically attempts to reconnect if the connection is lost.
   - The `onmessage` event handler processes incoming messages, which are parsed and displayed on the UI.
