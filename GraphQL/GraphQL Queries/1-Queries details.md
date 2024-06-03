# GraphQL Essentials

## Fields

At its simplest, GraphQL is about asking for specific fields on objects. Let's start by looking at a very simple query and the result we get when we run it:

This is a simple GraphQL query that retrieves the `name` field from the `hero` object.

**Example:**

```graphql
{
  hero {
    name
  }
}
```

**Result:**

The expected result of running this query would be:

```json
{
  "data": {
    "hero": {
      "name": "R2-D2"
    }
  }
}
```

You can see immediately that the query has exactly the same shape as the result. This is essential to GraphQL because you always get back what you expect, and the server knows exactly what fields the client is asking for. The `name` field returns a String type, in this case, the name of the main hero of Star Wars, "R2-D2".

[Source](https://graphql.org/learn/queries/#fields)

---

## Arguments

GraphQL allows passing arguments to fields, making data fetching much more powerful.

**Example:**

```graphql
{
  human(id: "1000") {
    name
    height
  }
}
```

**Result:**

The expected result of running this query would be:

```json
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 1.72
    }
  }
}
```

In REST, you can only pass a single set of arguments via query parameters and URL segments. In GraphQL, every field and nested object can have its own set of arguments, making it a complete replacement for making multiple API fetches. Arguments can be of various types; in the above example, we used an Enumeration type.

---

## Aliases

Aliases allow you to rename fields within your queries, improving readability, resolving conflicts, and reshaping data.

**Example:**

```graphql
{
  empireHero: hero(episode: EMPIRE) {
    name
  }
  jediHero: hero(episode: JEDI) {
    name
  }
}
```

**Result:**

The expected result of running this query would be:

```json
{
  "data": {
    "empireHero": {
      "name": "Luke Skywalker"
    },
    "jediHero": {
      "name": "R2-D2"
    }
  }
}
```

---

## Variables

Variables in GraphQL are placeholders within a query, filled with dynamic values from a separate dictionary.

**Dynamic Arguments:** Standard GraphQL queries include arguments directly within the string, but this becomes cumbersome for dynamic values like user selections or filters.

**Improved Approach:** Variables offer a separate mechanism to pass dynamic values as a dictionary, enhancing flexibility and code maintainability.

**Benefits:**

- Separates data from query structure, making queries cleaner and easier to manage.
- Simplifies client-side code by avoiding complex string manipulation.
- Promotes code reusability as queries can handle various inputs through variables.

- **Define the variable:**

```graphql
query GetEpisodeDetails($episodeNumber: Int!) {
  episode(episode: $episodeNumber) {
    title
    openingCrawl
  }
}
```

- **Provide the value separately:**

```javascript
const episodeNumber = userSelectedEpisode; // Assume this is retrieved from user input

fetch("/graphql", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({
    query: `query GetEpisodeDetails($episodeNumber: Int!) { ... }`, // Your query with variable
    variables: { episodeNumber }, // Pass the variable value here
  }),
})
  .then((response) => response.json())
  .then((data) => {
    // Use the fetched episode data
  });
```

### Default Variables

Default values can also be assigned to the variables in the query by adding the default value after the type declaration.

**Example:**

```graphql
query HeroNameAndFriends($episode: Episode = JEDI) {
  hero(episode: $episode) {
    name
    friends {
      name
    }
  }
}
```

---

## Fragments

GraphQL fragments are reusable units that let you define sets of fields to be fetched from your API, promoting code maintainability and reducing redundancy.

**Define the Fragment:** Create a named fragment specifying the fields you want to fetch from a particular GraphQL type.

**Include the Fragment:** Reference the fragment within your queries or mutations.

**Example:**

```graphql
{
  leftComparison: hero(episode: EMPIRE) {
    ...comparisonFields
  }
  rightComparison: hero(episode: JEDI) {
    ...comparisonFields
  }
}

fragment comparisonFields on Character {
  name
  appearsIn
  friends {
    name
  }
}
```

**Result:**

The expected result of running this query would be:

```json
{
  "data": {
    "leftComparison": {
      "name": "Luke Skywalker",
      "appearsIn": ["NEWHOPE", "EMPIRE", "JEDI"],
      "friends": [
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        },
        {
          "name": "C-3PO"
        },
        {
          "name": "R2-D2"
        }
      ]
    },
    "rightComparison": {
      "name": "R2-D2",
      "appearsIn": ["NEWHOPE", "EMPIRE", "JEDI"],
      "friends": [
        {
          "name": "Luke Skywalker"
        },
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        }
      ]
    }
  }
}
```

---

## Using Variables Inside Fragments

**Example:**

```graphql
query HeroComparison($first: Int = 3) {
  leftComparison: hero(episode: EMPIRE) {
    ...comparisonFields
  }
  rightComparison: hero(episode: JEDI) {
    ...comparisonFields
  }
}

fragment comparisonFields on Character {
  name
  friendsConnection(first: $first) {
    totalCount
    edges {
      node {
        name
      }
    }
  }
}
```

---

## Directives

In GraphQL, directives act like instructions that extend the functionality of the core language. They provide a way to attach metadata to various parts of your GraphQL schema or queries, influencing how the server interprets and executes them.

**Types of Directives:**

- **Built-in Directives:** Defined by the GraphQL specification and supported by all compliant GraphQL servers (e.g., `@skip`, `@include`, `@deprecated`).
- **Custom Directives:** Created specifically for a particular GraphQL service or tool, allowing for extending GraphQL's capabilities beyond the built-in options.

**What Directives Do:**

- **Modify Execution Behavior:** Directives can alter how the server processes your GraphQL requests (e.g., using `@skip` to conditionally exclude a field from the response).
- **Provide Type Validation:** Directives can enforce specific rules on your data schema.
- **Declare Server-Side Logic:** Schema directives can specify functionalities like authorization requirements or data formatting on the server-side.

**Where Directives Are Used:**

- **Schema (TypeSystem):** Applied to types, fields, arguments, and other elements within the GraphQL schema definition.
- **Queries (ExecutableDefinition):** Used within GraphQL queries or mutations, often attached to specific fields or fragments.
