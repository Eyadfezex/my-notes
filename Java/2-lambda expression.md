# What Are Lambda Expressions in Java?

A lambda expression is a short block of code that represents an **anonymous function** — a function with no name, that can be passed around like a value.

Introduced in **Java 8**, lambdas enable functional-style programming and dramatically reduce boilerplate code.

---

## Syntax

```java
(parameters) -> expression
(parameters) -> { statements; }
```

**Examples:**

```java
// No parameters
() -> System.out.println("Hello!")

// One parameter (parentheses optional)
x -> x * x

// Multiple parameters
(a, b) -> a + b

// Multi-line body
(a, b) -> {
    int result = a + b;
    return result;
}
```

---

## Functional Interfaces

Lambdas in Java work **only with functional interfaces** — interfaces that have exactly one abstract method.

| Interface           | Method        | Use Case                         |
| ------------------- | ------------- | -------------------------------- |
| `Runnable`          | `run()`       | Run code with no input/output    |
| `Callable<T>`       | `call()`      | Run code and return a value      |
| `Function<T, R>`    | `apply(T)`    | Transform input to output        |
| `Consumer<T>`       | `accept(T)`   | Take input, return nothing       |
| `Supplier<T>`       | `get()`       | Return a value, no input         |
| `Predicate<T>`      | `test(T)`     | Test a condition, return boolean |
| `BiFunction<T,U,R>` | `apply(T, U)` | Two inputs, one output           |

---

## Common Examples

**Runnable**

```java
// Before lambda
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Running!");
    }
};

// With lambda
Runnable r = () -> System.out.println("Running!");
```

**Sorting a list**

```java
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");

// Before lambda
Collections.sort(names, new Comparator<String>() {
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});

// With lambda
names.sort((a, b) -> a.compareTo(b));
```

**Filtering with Stream API**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
// [2, 4, 6]
```

**Transforming with map()**

```java
List<String> names = Arrays.asList("alice", "bob", "charlie");

List<String> upper = names.stream()
    .map(name -> name.toUpperCase())
    .collect(Collectors.toList());
// ["ALICE", "BOB", "CHARLIE"]
```

**Predicate**

```java
Predicate<Integer> isEven = n -> n % 2 == 0;
System.out.println(isEven.test(4)); // true
System.out.println(isEven.test(7)); // false
```

---

## Method References (shorthand for lambdas)

When a lambda just calls an existing method, you can shorten it with `::`.

```java
// Lambda
names.forEach(name -> System.out.println(name));

// Method reference (equivalent)
names.forEach(System.out::println);
```

| Type            | Syntax              | Equivalent Lambda          |
| --------------- | ------------------- | -------------------------- |
| Static method   | `ClassName::method` | `x -> ClassName.method(x)` |
| Instance method | `obj::method`       | `x -> obj.method(x)`       |
| Constructor     | `ClassName::new`    | `x -> new ClassName(x)`    |

---

## Variable Capture

Lambdas can access variables from the enclosing scope, but only if they are **effectively final** (not modified after assignment).

```java
String greeting = "Hello";
Runnable r = () -> System.out.println(greeting + ", World!");
r.run(); // Hello, World!

// This would cause a compile error:
// greeting = "Hi"; // ❌ cannot reassign after capture
```

---

## Lambda vs. Anonymous Class

|                | Lambda                     | Anonymous Class                      |
| -------------- | -------------------------- | ------------------------------------ |
| Verbosity      | Concise                    | Verbose                              |
| `this` keyword | Refers to enclosing class  | Refers to the anonymous class itself |
| Works with     | Functional interfaces only | Any interface or abstract class      |
| Performance    | Slightly better            | Slightly more overhead               |

---

## Summary

> Lambdas in Java let you write cleaner, shorter code by treating behavior as a value — especially powerful when combined with the **Stream API** and **functional interfaces**.
