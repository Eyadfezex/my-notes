# Subscriptions

GraphQL subscriptions are a powerful feature that enables real-time data updates between a GraphQL server and its clients. Unlike traditional GraphQL queries which only fetch data at a specific point in time, subscriptions establish a persistent connection allowing the server to push data updates to the subscribed clients as changes occur.

- **Client-side Setup:** Clients establish `subscriptions` by sending a GraphQL request with the subscription operation type. This request specifies the desired event (e.g., new message received) and the data to be included in the updates.

- **Real-time Updates:** The GraphQL server keeps the subscription connection open (often using WebSockets). Whenever the subscribed-to event occurs (e.g., a new message is received), the server actively pushes the relevant data to the subscribed clients.

Here are some common use cases for GraphQL subscriptions:

- **Chat applications:** Clients can subscribe to receive new messages as they are sent.
- **Social media feeds:** Updates to feeds or follower counts can be pushed to clients in real-time.
- **Live dashboards:** Stock prices, sensor readings, or other frequently changing data can be displayed with minimal latency.

---

## Event-based subscriptions

Event-based subscriptions are a mechanism in GraphQL that enables clients to receive real-time updates from the server based on specific events. These events can be triggered by various sources:

- User actions (e.g., creating a post, sending a message)
- Sensor data updates (e.g., temperature change, stock level)
- External system interactions (e.g., payment confirmation, social media activity)
- Internal server actions (e.g., database updates, background tasks)
