# Decorators

In TypeScript, decorators are a special syntax that allows you to add annotations and modify the behavior of classes, properties, methods, and other parts of your code. They are essentially functions that are executed at compile time, giving you more control over your code structure and functionality.

**What can be decorated?**

- **Classes:** You can decorate class declarations to observe, modify, or even replace the class definition entirely.

```ts
function logClass(target: any) {
  console.log(`Class ${target.name} is instantiated`);
}

@logClass
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const person = new Person("Alice"); // This line triggers the decorator
```

---

- **Methods:** Method decorators are applied to method declarations and can be used to observe, modify, or replace the method's behavior.

```ts
function logMethod(
  target: any,
  propertyKey: string,
  descriptor: PropertyDescriptor
) {
  const originalMethod = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`Calling method ${propertyKey} with arguments:`, args);
    return originalMethod.apply(this, args);
  };
  return descriptor;
}

class Math {
  @logMethod
  add(a: number, b: number): number {
    return a + b;
  }
}

const math = new Math();
math.add(2, 3); // This call triggers the decorator
```

---

- **Properties:** Property decorators target class properties and allow you to manipulate how the property is defined or interact with its setter/getter.

```ts
function stringValidator(target: any, propertyKey: string) {
  let value: string;
  const setter = function (newValue: any) {
    if (typeof newValue === "string") {
      value = newValue;
    } else {
      console.error(
        `Invalid value for property ${propertyKey}, expected string`
      );
    }
  };

  const getter = function () {
    return value;
  };

  Object.defineProperty(target, propertyKey, {
    get: getter,
    set: setter,
  });
}

class User {
  @stringValidator
  name: string;
}

const user = new User();
user.name = "John"; // Valid assignment
user.name = 10; // Triggers error in console
```

---

- **Accessors:** Similar to properties, decorators can be applied to accessors (getters and setters) to modify their behavior.

```ts
function logGet(
  target: any,
  propertyKey: string,
  descriptor: PropertyDescriptor
) {
  const getter = descriptor.get;
  if (getter) {
    descriptor.get = function () {
      console.log(`Getting value of property ${propertyKey}`);
      return getter.call(this);
    };
  }
  return descriptor;
}

class Product {
  private _price: number;

  @logGet
  get price(): number {
    return this._price;
  }

  set price(value: number) {
    this._price = value;
  }
}

const product = new Product();
product.price = 10; // Doesn't trigger log (setter)
console.log(product.price); // Triggers log (getter)
```
