# Advanced Types

Advanced types in TypeScript are a set of advanced type constructs that allow for more complex and expressive type systems.

## Mapped Types

Imagine you have a type that defines the structure of something, like a user profile. This type might specify properties like name, email, and age. Mapped types let you take this existing type and create a new one based on it. In the new type, you can modify the properties in some way, like making them all optional or converting them to strings.

- **How Mapped Types Work:**

  - **Source Type:** You start with an existing type that defines the structure you want to modify.
  - **Transformation:** You define a rule or function that specifies how to change the properties of the source type. This can involve things like making them optional, changing their types, or adding prefixes.
  - **New Type Creation:** Based on the source type and the transformation rule, a new type is created with the modified properties.

**Example:**

```ts
type Address = {
  street: string;
  city: string;
  state: string;
  zip: string;
};

// Mapped type to make all properties read-only
type ReadOnlyAddress = {
  readonly [key in keyof Address]: Address[key];
};

// Function to create a read-only address
function createAddress(
  street: string,
  city: string,
  state: string,
  zip: string
): ReadOnlyAddress {
  return { street, city, state, zip };
}

// Usage
const myAddress = createAddress("123 Main St", "Anytown", "CA", "12345");
console.log(myAddress); // { street: "123 Main St", city: "Anytown", state: "CA", zip: "12345" }

// Attempting to modify a property will result in a compilation error
// myAddress.street = "New Street"; // Error: cannot assign to 'street' because it is read-only
```

---

## Conditional Types

Conditional types in TypeScript are a way to select a type based on a condition. They allow you to write a type that dynamically chooses a type based on the types of its inputs. Conditional types are declared using a combination of the infer keyword and a type that tests a condition and selects a type based on the result of the test.

- **How Conditional Types Work:**

  - **Condition:** You define a condition that evaluates to either true or false. This condition can involve checking property types, comparing values, or using other type predicates.
  - **Type if True:** You specify the type that will be used if the condition evaluates to true.
  - **Type if False:** You define the type that will be used if the condition evaluates to false.

**Example:**

```ts
type ParseResult<T> = T extends string | number
  ? T extends number
    ? number
    : string
  : never;

function parseValue(value: string): ParseResult<typeof value> {
  const parsedNumber = parseFloat(value);
  return isNaN(parsedNumber) ? value : parsedNumber;
}

const numResult = parseValue("123"); // numResult: number
const strResult = parseValue("abc"); // strResult: string

// Providing an invalid type will result in a compilation error
// const invalidResult = parseValue(true); // Error: Type 'true' does not satisfy condition
```

---

## Literal Types

In TypeScript, literal types let you define a type that only accepts a specific literal value. This can be useful for things like:

```ts
type CardinalDirection = "North" | "East" | "South" | "West";

function move(distance: number, direction: CardinalDirection) {
  // ...
}

move(1, "North"); // Okay
move(1, "Nurth"); // Error!  "Nurth" is not a valid direction

//--------------------------------------------

type StatusCode = 200 | 404 | 500;

function handleResponse(code: StatusCode) {
  // Handle response based on the exact status code
}

handleResponse(200); // OK
handleResponse(301); // Error!  301 is not a defined status code
```

- **Template Literal Types**
  Template literal types in TypeScript are a way to manipulate string values as types. They allow you to create a type based on the result of string manipulation or concatenation.

```ts
type Name = `Mr. ${string}`;

let name: Name = `Mr. Smith`; // ok
let name: Name = `Mrs. Smith`; // error
```

---

## Recursive Types

In TypeScript, recursive types allow you to define a type that refers to itself within its definition. This is particularly useful for modeling data structures with nested elements, such as:

- Linked lists
- Trees
- Hierarchical data

Here's a breakdown of key concepts and examples:

**Core Idea:**

A recursive type relies on circular referencing. The type definition itself includes the type it's defining. This might sound confusing, but it becomes clear with examples.

**Common Use Cases:**

- **Linked Lists:** A linked list node can hold data and a reference to the next node in the list. The next node itself can also be a linked list node.

```typescript
type ListNode<T> = {
  data: T;
  next?: ListNode<T>;
};

const head: ListNode<number> = { data: 1, next: { data: 2, next: null } };
```

- **Trees:** A tree node can have data and an array of child nodes, where each child node can also be a tree node of the same type.

```typescript
type TreeNode<T> = {
  data: T;
  children?: TreeNode<T>[];
};

const tree: TreeNode<string> = {
  data: "Root",
  children: [
    { data: "Child 1", children: [] },
    { data: "Child 2", children: [{ data: "Grandchild", children: [] }] },
  ],
};
```

**Benefits:**

- **Improved Type Safety:** Ensures data structures have the expected nested structure during development, preventing runtime errors.
- **Readability:** Clearly defines the structure of complex data by allowing the type to reflect the nesting.

**Things to Consider:**

- **Potential for Infinite Types:** Be cautious of creating circular references that could lead to infinitely nested types. TypeScript has a recursion limit to prevent this.
- **Readability for Complex Types:** Overly complex recursive types can be hard to understand. Use clear names and comments for better maintainability.

**Overall, recursive types are a powerful tool in TypeScript for defining and working with nested data structures. By understanding their concepts and limitations, you can leverage them to create type-safe and well-structured code.**
