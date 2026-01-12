# What is polling?

Polling is a technique where the client repeatedly requests the server to check if a specific operation has been completed. The client asks the server at regular intervals, and the server responds with the current status.

There are two types of polling:

- **Short polling**:

  **Pros:**

  - Simple to implement
  - Suitable for monitoring long-running operations
  - Allows the client to disconnect and reconnect without issues

  **Cons:**

  - Can generate excessive network traffic ("chatty")
  - Consumes unnecessary bandwidth
  - Can waste backend resources due to frequent requests
