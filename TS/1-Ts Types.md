# TypeScript Types

Typescript adds static type checking to JavaScript, which means you can define the data types of your variables and functions before you run your code.

## Primitive Types

- `boolean`: Same as JavaScript, represents logical values (`true` or `false`).
- `number`:Same as JavaScript, represents numeric values.
- `string`: Same as JavaScript, represents sequences of characters.
- `undefined`: Same as JavaScript, represents a declared variable without a value.
- `null`:Same as JavaScript, represents the intentional absence of a value.

```ts
let age: number = 35; // Number (integer)
let name: string = "Bob"; // String
let isStudent: boolean = true; // Boolean (true/false)

let nothing: undefined; // Undefined (variable declared without a value)
let nothingElse: null = null; // Null (intentional absence of a value)

console.log(age, name, isStudent, nothing, nothingElse);
```

---

## Object Types

- `interface`:Defines the structure (properties and types) an object must follow.

```ts
interface Person {
  name: string;
  age: number;
}

const user: Person = {
  name: "Alice",
  age: 30,
};

console.log(user.name); // Output: "Alice"
```

- `Class`:A blueprint for creating objects with properties and methods.

```ts
class Car {
  model: string;
  year: number;

  constructor(model: string, year: number) {
    this.model = model;
    this.year = year;
  }

  getDetails() {
    return `This is a ${this.year} ${this.model} car.`;
  }
}

const myCar = new Car("Corolla", 2023);
console.log(myCar.getDetails()); // Output: "This is a 2023 Corolla car."
```

- `Enum`:A set of named constants for fixed values (e.g., colors, days of the week).

```ts
enum Color {
  Red,
  Green,
  Blue,
}

let favoriteColor: Color = Color.Green;
console.log(favoriteColor); // Output: 1 (Green's numerical value)
```

- `Array`:An ordered collection of elements, all of the same or compatible types.

```ts
let numbers: number[] = [1, 2, 3, 4, 5];
console.log(numbers[2]); // Output: 3

let colors: string[] = ["red", "green", "blue"];
console.log(colors.length); // Output: 3
```

- `Tuple`: A specific type of array where each position has a predefined type.

```ts
let employee: [string, number, boolean] = ["John Doe", 35, true];
console.log(employee[1]); // Output: 35 (number at index 1)

// Compile-time error: trying to assign a different type to a tuple position
// employee[0] = 10; // This would cause an error
```

---

## Other Types

- `any`: Escape hatch for any value type, use cautiously.
- `object`: Generic object type, less type safety than interfaces/classes.
- `unknown`: Type for unknown values, requires type checking before use.
- `never`: Represents a type that never occurs (functions that throw errors or never return).

---

## Type Assertions

In TypeScript, type assertions are a mechanism that allows you to tell the compiler to treat a value as a specific type. It's essentially a way to override the compiler's inferred type for a variable.

- **Purpose**: Used when the compiler can't infer the correct type or when you have a better understanding of the value's type than the compiler does.

- **Syntax**: There are two ways to perform type assertions:
  - Angle bracket syntax: `let value: number = <number>myUnknownValue;`
  - `as` keyword syntax: `let value: number = myUnknownValue as number;`

```ts
let userInput: string | number = prompt("Enter a number:");

// userInput could be a string or a number

if (typeof userInput === "string") {
  // Handle string input
  let convertedNumber = parseInt(userInput); // Might cause errors if not a valid number
  console.log(`You entered: ${convertedNumber}`);
} else {
  // Use type assertion assuming it's actually a number
  let numberValue = userInput as number;
  console.log(`You entered: ${numberValue}`);
}
```

**As Const:**

`as const` is a type assertion in TypeScript that allows you to assert that an expression has a specific type, and that its value should be treated as a read-only value.

```ts
const colors = ["red", "green", "blue"] as const;

// colors is now of type readonly ['red', 'green', 'blue']
```

---

## Type Inference

Type inference is a powerful feature in TypeScript that allows the compiler to automatically deduce the type of a variable or expression based on its initialization or usage.

```ts
let name = "John Doe";
// he TypeScript compiler automatically infers that the type of the name variable is string.
```

---

## Type Compatibility

- **Structural Typing:** Types are compatible based on their structure (properties and their types) rather than their names.
- **Assignment Compatibility:** A wider type (like `any`) can hold values of narrower types (like `number`).
- **Object Compatibility:** An object can be assigned if it has at least the same properties (with compatible types) as the target type.
- **Function Compatibility:** Functions are compatible if their parameter and return types align.
