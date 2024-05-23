# Generics

Generics are a powerful feature in TypeScript that allow you to write code that can work with different types of data. They essentially act as templates for functions, classes, and interfaces that can be reused with various data types.

## Generic Types

Generic types in TypeScript allow you to write objects, functions and classes that work with multiple data types, instead of being limited to a single data type. A generic type is defined using angle brackets `<T>` and can be used as a placeholder for a specific data type.

- **Examples of Generics in TypeScript:**

  - Generic Function:

  ```ts
  function identity<T>(arg: T): T {
    return arg;
  }

  let stringIdentity = identity<string>("Hello");
  let numberIdentity = identity<number>(100);
  ```

  - Generic Class:

  ```ts
  class GenericArray<T> {
    private items: T[] = [];

    add(item: T) {
      this.items.push(item);
    }

    get(index: number): T {
      return this.items[index];
    }
  }

  let stringArray = new GenericArray<string>();
  stringArray.add("apple");
  stringArray.add("banana");

  let numberArray = new GenericArray<number>();
  numberArray.add(1);
  numberArray.add(2);
  ```

## Generic Constraints

Generic constraints in TypeScript allow you to restrict the types that can be used with a generic function, class, or interface. This adds more control and type safety to your code.

- **Concept:**

  - By default, generic types in TypeScript can be any data type.
  - Constraints allow you to specify that the generic type parameter must inherit from a certain class, implement a specific interface, or fulfill other conditions.
  - This ensures that the generic code only works with types that have the required functionalities.
    <br>

- **Using Generic Constraints:**

```ts
interface Printable {
  print(): void;
}

function printIt<T extends Printable>(arg: T) {
  arg.print();
}
```

```ts
class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

function greet<T extends Person>(person: T) {
  console.log("Hello, " + person.name);
}
```
