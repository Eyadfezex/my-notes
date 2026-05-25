# Static vs Non-Static in Java

## What is the `static` Keyword?

In Java, the `static` keyword is used to indicate that a particular member (variable, method, block, or nested class) belongs to the class itself, not to any instance of the class.

**Key points about static members:**

- Static members are shared across all instances of a class.
- Memory for static members is allocated once, when the class is loaded by the JVM.
- Static members can be accessed directly using the class name (e.g., `ClassName.staticMember`), without needing to create an object.
- Static methods and variables cannot directly access non-static (instance) members, because non-static members require an instance.
- Static methods cannot be overridden in the same way as instance methods; static methods are resolved at compile time and are associated with the class, not with an object.

> **Note:** When a subclass declares a static method with the same signature as one in its superclass, the method in the subclass hides the superclass method—it does not override it. This is called method hiding. The `@Override` annotation cannot be used with static methods.

Example:

```java
class SuperClass {
    public static void staticMethod() {
        System.out.println("SuperClass: inside staticMethod");
    }
}

public class SubClass extends SuperClass {
    // This hides the staticMethod in SuperClass (method hiding)
    public static void staticMethod() {
        System.out.println("SubClass: inside staticMethod");
    }

    public static void main(String[] args) {
        SuperClass superClassWithSuperCons = new SuperClass();
        SuperClass superClassWithSubCons = new SubClass();
        SubClass subClassWithSubCons = new SubClass();

        superClassWithSuperCons.staticMethod();      // SuperClass: inside staticMethod
        superClassWithSubCons.staticMethod();        // SuperClass: inside staticMethod (method hiding, not overriding)
        subClassWithSubCons.staticMethod();          // SubClass: inside staticMethod
    }
}
```

---

## Non-Static Members

Non-static (also called instance) members are tied to a specific object of the class. Each created object gets its own copy of instance variables, and instance methods can access both static and non-static members of the class.
