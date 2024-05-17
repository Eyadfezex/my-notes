# Type Guards in TypeScript

Type guards are powerful tools in TypeScript that enable you to refine the type of a variable at runtime within a specific block of code. They essentially perform checks to determine the exact type of a value and inform the compiler to adjust its understanding of that variable's type accordingly. This leads to more type-safe and predictable code.

**Common Type Guards:**

1. **`typeof` Operator:**

   - A fundamental type guard for checking primitive types like `string`, `number`, `boolean`, and `symbol`.
   - It returns a string representing the type of the value being checked.

   ```ts
   function processValue(value: unknown): void {
     if (typeof value === "string") {
       console.log(`Value is a string: ${value}`);
     } else if (typeof value === "number") {
       console.log(`Value is a number: ${value}`);
     } else {
       // Handle other types (or throw an error)
     }
   }
   processValue("Hello World!"); // Output: Value is a string: Hello World!
   processValue(10); // Output: Value is a number: 10
   processValue(true); // Currently no output for booleans (add logic for handling)
   ```

2. **`instanceof` Operator:**

   - Ideal for working with classes and object hierarchies.
   - Checks whether an object is an instance of a specific class.

```ts
// Base class representing a generic animal
class Animal {}

// Class representing a dog, inherits from Animal
class Dog extends Animal {}

// Function to make an animal sound
function makeSound(animal: Animal): void {
  // Check if the animal is a Dog using instanceof
  if (animal instanceof Dog) {
    console.log("Woof!");
  } else {
    console.log("Generic animal sound");
  }
}

// Create a Dog object
const myDog = new Dog();

// Make the dog sound
makeSound(myDog); // This will print "Woof!"

// Create another animal object (not a dog)
const anotherAnimal = new Animal();

// Make the other animal sound
makeSound(anotherAnimal); // This will print "Generic animal sound"
```

3. **Equality Checks (`===` and `!==`)** (Use with Caution):

- While not always the most reliable due to potential type coercion, equality checks can be used as type guards in certain scenarios.
- Be cautious of implicit type conversion that might lead to unexpected results.

```ts
function greetUser(user: unknown): void {
  if (user !== null && typeof user === "object") {
    // TypeScript now knows user is likely an object with a name property
    console.log(`Hello, ${user.name}!`);
  } else {
    console.log("Invalid user object");
  }
}

// Example 1: Valid user object with name property
const validUser = { name: "Alice" };
greetUser(validUser); // This will print "Hello, Alice!"

// Example 2: Invalid user object (null)
greetUser(null); // This will print "Invalid user object"

// Example 3: Invalid user object (not an object)
greetUser(10); // This will print "Invalid user object"
```

4. **Truthiness Checks** (Limited Use Cases):

   - In some cases, checking for truthiness (if (value)) or falsiness (if (!value)) can act as a type guard, primarily for boolean values.
   - However, this approach can be less type-safe as non-boolean values can also be truthy or falsy. Use with caution.

**Choosing the Right Type Guard:**

- **Primitive Types:** `typeof` is the go-to choice.
- **Class Hierarchies:** `instanceof` is the most suitable option.
- **Complex Type Checks:** Consider custom type predicates for more flexibility and control.
- **Truthiness/Falsiness:** Use sparingly due to potential type coercion issues.

**Additional Considerations:**

- Type predicates offer a powerful way to define custom type checks that can handle more complex scenarios.
- Always strive for type safety, and use type guards judiciously when necessary.

By effectively using type guards, you can enhance the type safety and clarity of your TypeScript code, making it easier to reason about and maintain.
