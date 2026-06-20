# What is Optional?

`Optional` is a way invented to solve the problem of **null returns**. Sometimes when you implement a function that queries something, there's always a scenario where it could return null (e.g. a database lookup that finds nothing). `Optional` was made to handle that — it forces you to deal with the "missing value" case explicitly instead of accidentally hitting a `NullPointerException`.

```java
// Without Optional — risky
public User findUserById(int id) {
    return database.lookup(id); // might return null
}

User user = findUserById(5);
user.getName(); // NullPointerException if user is null!
```

```java
// With Optional — explicit
public Optional<User> findUserById(int id) {
    User user = database.lookup(id);
    return Optional.ofNullable(user);
}
```

---

## Creating an Optional

```java
Optional<String> a = Optional.of("hello");       // value must NOT be null
Optional<String> b = Optional.empty();            // explicitly empty
Optional<String> c = Optional.ofNullable(maybe);  // empty if null, present otherwise
```

> `Optional.of(null)` throws `NullPointerException` immediately — use `ofNullable` when the value might be null.

---

## Checking and getting the value

```java
Optional<String> opt = Optional.of("hi");

opt.isPresent();   // true if a value exists
opt.isEmpty();     // true if empty (Java 11+)

opt.get();         // returns "hi", throws NoSuchElementException if empty — avoid using directly
```

---

## Safer ways to extract values

```java
// 1. Provide a default
String name = opt.orElse("default");

// 2. Compute a default lazily (only runs if empty)
String name = opt.orElseGet(() -> computeDefault());

// 3. Throw a custom exception if empty
String name = opt.orElseThrow(() -> new IllegalStateException("missing"));

// 4. Run code only if present
opt.ifPresent(value -> System.out.println(value));

// 5. Run code if present, or something else if empty (Java 9+)
opt.ifPresentOrElse(
    value -> System.out.println(value),
    () -> System.out.println("nothing here")
);
```

---

## Transforming values: `map` and `filter`

```java
Optional<String> name = Optional.of("claude");

Optional<Integer> length = name.map(String::length); // Optional[6]

Optional<String> startsWithC = name.filter(n -> n.startsWith("c")); // Optional[claude]
Optional<String> startsWithX = name.filter(n -> n.startsWith("x")); // Optional.empty
```

Chaining transformations without manual null checks at each step:

```java
Optional<User> userOpt = findUserById(5);

String city = userOpt
    .map(User::getAddress)
    .map(Address::getCity)
    .orElse("Unknown");
```

If any step is empty, the chain short-circuits to empty — no NPE.

---

## `flatMap` for nested Optionals

If a method already returns an `Optional`, use `flatMap` instead of `map` to avoid `Optional<Optional<T>>`:

```java
public Optional<Address> getAddress() { ... }

Optional<Address> address = userOpt.flatMap(User::getAddress);
```

---

## Best practices

- **Use `Optional` as a return type**, not as a field, method parameter, or inside collections. It's meant to communicate "this method might not return a value."
- **Never call `.get()` without checking presence** — prefer `orElse` / `orElseThrow` / `map` instead.
- **Don't overuse it** — primitives and simple internal logic don't need wrapping in `Optional`.
- For primitives, use `OptionalInt`, `OptionalLong`, `OptionalDouble` to avoid boxing overhead.

---

## Full example

```java
public Optional<String> findEmail(int userId) {
    return userRepository.findById(userId)
        .map(User::getEmail)
        .filter(email -> !email.isBlank());
}

String email = findEmail(42).orElse("no-email@example.com");
```
