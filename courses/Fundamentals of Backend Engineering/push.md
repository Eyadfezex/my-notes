# What is Push?

In backend engineering, **push** is a communication pattern where both the server and the client can send data to each other, often without explicit requests. This enables ongoing, real-time communication—such as notifications, live data feeds, or chat systems—where updates can flow from server to client and client to server as needed.

Pros:

- Real-time updates

Cons:

- Client must be online
- Client may not be able to handle the data
- Requires a bidirectional protocol

Polling is preferred for lightweight clients.
