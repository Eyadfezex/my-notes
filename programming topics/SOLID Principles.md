# 💡 S.O.L.I.D Principles: Building Better Software

---

## 1. **S — Single Responsibility Principle (SRP)**

> _"A class should have one, and only one, reason to change."_

- Each class/module/function should **do one thing only** and do it well.
- It's about **separation of concerns** and maintaining focus.
- ✅ Good:
  - `UserService` handles user authentication and profile management
  - `EmailService` handles email composition and delivery
- ❌ Bad:
  - `UserManager` that handles registration, emails, logging, and payment processing
- 🔑 Key benefit: Easier maintenance, testing, and reduced coupling

---

## 2. **O — Open/Closed Principle (OCP)**

> _"Software entities should be open for extension, but closed for modification."_

- Design your code to **welcome new features** without disturbing existing functionality.
- Leverage **abstraction** through:
  - Interfaces
  - Abstract classes
  - Polymorphism
- ✅ Best practices:
  - Use strategy pattern for swappable behaviors
  - Implement plugin architectures
  - Design with extension points in mind
- 📝 Example: Payment system

  ```typescript
  abstract class PaymentProcessor {
    abstract process(amount: number): void;
  }

  class StripeProcessor extends PaymentProcessor { ... }
  class PayPalProcessor extends PaymentProcessor { ... }
  ```

---

## 3. **L — Liskov Substitution Principle (LSP)**

> _"Subtypes must be substitutable for their base types."_

- If class `S` extends class `T`, any code working with `T` should work seamlessly with `S`.
- ✅ Good practices:
  - Respect the contract defined by the base class
  - Maintain invariants when inheriting
  - Follow "is-a" relationship strictly
- ❌ Common violations:
  - Throwing unexpected exceptions
  - Breaking parameter constraints
  - Violating method behavior expectations
- 🎯 Example:

  ```typescript
  // Valid LSP
  class Bird {
    makeSound(): string {
      return "chirp";
    }
  }
  class Sparrow extends Bird {
    makeSound(): string {
      return "tweet";
    }
  }
  ```

---

## 4. **I — Interface Segregation Principle (ISP)**

> _"Clients should not be forced to depend on interfaces they do not use."_

- Create **focused, minimal interfaces** instead of large, monolithic ones
- Benefits:
  - Reduced coupling
  - Better testability
  - More flexible implementation
- ✅ Example:

  ```typescript
  // Instead of one large interface:
  interface Bird {
    fly();
    walk();
    swim();
  }

  // Break it down:
  interface Flyable {
    fly();
  }
  interface Walkable {
    walk();
  }
  interface Swimmable {
    swim();
  }
  ```

---

## 5. **D — Dependency Inversion Principle (DIP)**

> _"Depend on abstractions, not concretions."_

- High-level modules should depend on abstractions
- Low-level modules should implement those abstractions
- Key practices:
  - Use dependency injection
  - Program to interfaces
  - Implement IoC containers when needed
- 🔧 Implementation example:

  ```typescript
  // Instead of:
  class UserService {
    private db = new MySQLDatabase();
  }

  // Do:
  class UserService {
    constructor(private database: IDatabase) {}
  }
  ```

---

## TL;DR with a Vibe

| Principle | Vibe        | You Should...                         | Key Benefit                   |
| --------- | ----------- | ------------------------------------- | ----------------------------- |
| SRP       | Focused     | Keep classes clean & single-purpose   | Maintainable & testable code  |
| OCP       | Unbreakable | Add features without breaking stuff   | Scalable architecture         |
| LSP       | Reliable    | Trust subclasses to behave right      | Predictable inheritance       |
| ISP       | Lightweight | Don't force code to carry dead weight | Flexible & modular interfaces |
| DIP       | Flexible    | Rely on contracts, not specific tools | Decoupled & adaptable systems |

---

## 🎯 Pro Tips

1. Start with SRP as your foundation
2. Use OCP when planning for future extensions
3. Apply LSP when designing inheritance hierarchies
4. Consider ISP when defining interfaces
5. Implement DIP to achieve loose coupling

Remember: SOLID principles are guidelines, not rules. Apply them pragmatically based on your specific context and needs.
