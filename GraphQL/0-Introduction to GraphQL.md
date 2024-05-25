# intro to GraphQL

**Overview**
GraphQL is a query language for your API, and a server-side runtime for executing queries using a **type system** you define for your data. GraphQL isn’t tied to any specific database or storage engine and is instead backed by your existing code and data.

## Problems GraphQL Solves

GraphQL solves several problems commonly faced in API development and consumption, particularly those associated with more traditional RESTful services.

- **Overfetching and Underfetching Data:**
  With REST APIs, clients often have to make multiple requests to fetch all the data they need for a single view on the frontend. This can lead to overfetching, where the client receives more data than it needs, or underfetching, where the client doesn't get enough data and has to make additional requests. GraphQL allows clients to specify exactly the data they need in a single request, eliminating these inefficiencies.

- **Complex Queries:**
  REST APIs can become cumbersome when dealing with complex data relationships that require joining data from multiple endpoints. GraphQL provides a powerful query language that allows clients to request data from multiple resources in a single query, making it easier to retrieve complex data structures.

- **Data Consistency:**  
  In REST APIs, data updates might require changes to multiple endpoints to ensure consistency. GraphQL offers a mechanism to ensure that all requested data reflects the latest state in the backend, simplifying data management.

- **Client-side Caching:**
  Since GraphQL queries explicitly define the data requirements, clients can effectively cache the fetched data. This can improve performance by reducing the number of API calls needed for subsequent requests with overlapping data.

---

## Thinking in Graphs

Graphs are powerful tools for modeling many real-world phenomena because they resemble our natural mental models and verbal descriptions of the underlying process. With GraphQL, you model your business domain as a graph by defining a schema; within your schema, you define different types of nodes and how they connect/relate to one another. On the client, this creates a pattern similar to Object-Oriented Programming: types that reference other types. On the server, since GraphQL only defines the interface, you have the freedom to use it with any backend (new or legacy!).
