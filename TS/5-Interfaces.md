# Interfaces in TypeScript

Interfaces in TypeScript define a contract for a type, outlining a set of expected properties, methods, and events. They act as blueprints for objects, classes, and function arguments, enforcing a specific structure that your code must adhere to. Interfaces themselves aren't included in the transpiled JavaScript; they serve as a type-checking mechanism during TypeScript compilation.

**Example:**

```typescript
interface Person {
  name: string;
  age: number;
}

function greet(person: Person): string {
  return "Hello " + person.name;
}
```

---

## Types vs. Interfaces

Both interfaces and types serve the purpose of defining data structures in TypeScript, enhancing code readability and enabling early error detection by guaranteeing variables and functions work with the anticipated data format.

**Types:**

- **Flexibility:** Can define a broader range of data types, including primitives (string, number, boolean), unions (multiple possible types), intersections (combinations of types), tuples (ordered arrays with specific types), and even references to other types.
- **Simple Syntax:** Utilize the `type` keyword followed by the desired name and type definition.
- **Limitations:** Cannot be extended or merged with other types.

**Interfaces:**

- **Object Focus:** Primarily used to describe object structures, specifying properties (name-value pairs) and their corresponding data types.
- **Object-Oriented Style:** The syntax resembles defining a class blueprint, using the `interface` keyword.
- **Extensible:** Interfaces can inherit properties from existing interfaces through the `extends` keyword, promoting code reuse.
- **Mergeable:** Interfaces can be declared multiple times with additional properties, which are merged into a single interface definition.

**Example:**

```typescript
// Type for a point with coordinates
type Point = { x: number; y: number };

// Interface for a user with name and age
interface User {
  name: string;
  age: number;
}

// Extending another interface
interface Admin extends User {
  role: string;
}
```

---

## Extending Interfaces

TypeScript allows extending interfaces by creating a new interface that inherits from the original one using the `extends` keyword.

```typescript
interface Shape {
  width: number;
  height: number;
}

interface Square extends Shape {
  sideLength: number;
}

let square: Square = {
  width: 10,
  height: 10,
  sideLength: 10,
};
```

---

## Hybrid Types

In TypeScript, hybrid types combine multiple types into a single type definition.

```typescript
type StringOrNumber = string | number;
```
