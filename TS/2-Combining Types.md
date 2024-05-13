# Combining Types

In TypeScript, combining types refers to creating new, more complex types from existing ones. There are two main ways to achieve this:

- **Union Types:** These are formed using the pipe symbol (`|`). A union type allows a variable to hold a value of any of the types included in the union. For instance, you could create a union type `name: string | number` that could hold either a string or a number representing a name. This is useful for situations where you expect input in various formats or want to provide flexibility in function arguments.

```ts
type Outcome = "success" | "failure";

let result: Outcome;
result = "success"; // Valid
result = "failure"; // Also valid
// result = 42;        // Error: Not a valid outcome type
```

- **Intersection Types:** Represented by the ampersand symbol (`&`), intersection types combine multiple types into a single one. A variable with an intersection type must have all the properties of each type involved. Imagine an intersection type `Profile & Serializable`, where `Profile` defines user properties and `Serializable` specifies how to format the data for storage. This creates a type requiring a profile that can also be serialized.

Here's a breakdown of the key differences:

| Feature        | Union Types (`\|`)                                  | Intersection Types (`&`)                                  |
| -------------- | --------------------------------------------------- | --------------------------------------------------------- |
| Resulting Type | A variable can be of any type in the union.         | A variable has all properties from all combined types.    |
| Use Case       | When expecting different input formats or           | When needing a value with properties from multiple types. |
| Example        | `string \| number` (name can be a string or number) | `Profile & Serializable` (profile with serialization)     |

- **Type Aliases:** type aliases provide a way to create more readable and meaningful names for existing types. They act like nicknames, making your code easier to understand and maintain.

```ts
type CarYear = number;
type CarModel = string;

type Car = {
  year: CarYear;
  model: CarModel;
};

const myCar: Car = {
  year: 2024,
  model: "Corolla",
};
```

- **`keyof` Operator:** The `keyof` operator in TypeScript is a powerful tool for working with object types. It allows you to extract the set of all keys (property names) from an object type and turn them into a new type.

```ts
interface Person {
  name: string;
  age: number;
  isActive: boolean;
}

type PersonKeys = keyof Person; // PersonKeys is now "name" | "age" | "isActive"

let key: PersonKeys;
key = "name"; // Valid (key is of type "name")
key = "age"; // Also valid
// key = 42;      // Error: Not a valid key type (should be a string from Person)
```
