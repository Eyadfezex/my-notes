# Functions

TypeScript functions are fundamental building blocks for creating well-structured and maintainable code.

**Function Definition:**

```ts
function functionName(
  argument1: type1,
  argument2: type2,
  ...argumentN: typeN
): returnType {
  // Function body with statements
}
```

---

## Function Overloading

In TypeScript, function overloading allows you to define multiple function signatures with the same name but different argument lists. This enables a single function to exhibit varying behaviors based on the types and number of arguments provided when it's called.

```ts
function makeSound(animal: string): string;
function makeSound(animal: Dog): string;

function makeSound(animal: any): string {
  if (typeof animal === "string") {
    return `A ${animal} makes a generic sound`;
  } else if (animal instanceof Dog) {
    return "Woof!";
  } else {
    return "Unknown animal sound";
  }
}

// Valid calls based on function signatures
const catSound = makeSound("cat");
const dogSound = makeSound(new Dog());

// Invalid call (won't match any signature)
// const numberSound = makeSound(10);
```
