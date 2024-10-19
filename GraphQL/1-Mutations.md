# Mutations

In GraphQL, mutations are essentially tools for modifying data within your underlying data sources. They act as counterparts to queries, which are used for fetching data. Here's a breakdown of what mutations are and how they function:

**Purpose:**

- Unlike queries that retrieve data, mutations allow you to create, update, or delete data in your graph.
- They provide a central point for making changes to your data through a GraphQL API.

**How it Works:**

- Mutations are defined within the GraphQL schema, similar to how queries are.
- They are denoted by the `mutation` keyword.
- Each mutation typically has a name that reflects its purpose (e.g., `createUser`, `updatePost`).
- Mutations can accept arguments, which specify the data to be modified.
- They may return data, such as the newly created or updated information.

```graphql
# This mutation creates a new todo item.
mutation CreateTodo {
  # Creates a new todo with the specified title.
  createTodo(title: "Write a blog post", completed: false) {
    # Unique identifier of the newly created todo item.
    id
    # Title of the todo item.
    title
    # Indicates whether the todo item is completed or not.
    completed
  }
}
```
