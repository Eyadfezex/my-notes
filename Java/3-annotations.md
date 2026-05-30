# What Are Annotations in Java?

Annotations are special forms of metadata in Java. They are a way to attach additional information to your code – for example, to a class, method, or variable – without changing what the code does when it runs. The most common use is for the compiler and simple tools.

---

## How to Create an Annotation

You can define your own annotation using the `@interface` keyword, like this:

```java
public @interface MyAnnotation {
}
```

### Rules for Annotations

1. **Allowed Types:**  
   The elements (similar to methods) inside your annotation can only be primitives (int, boolean, etc.), `String`, `Class`, enums, other annotations, or arrays of these types.

   ```java
   public @interface MyAnnotation {
       String name();
       int count() default 1;
       Class<?> type();
   }
   ```

2. **No Parameters or Exceptions:**  
   The elements cannot take parameters or throw exceptions. For example, **not allowed:**

   ```java
   String value(String arg); // NOT allowed
   ```

3. **No Method Bodies:**  
   The elements cannot contain any code.

   ```java
   String value() { return "x"; } // NOT allowed
   ```

4. **Default Values:**  
   You can give an element a default value using the `default` keyword.

   ```java
   int priority() default 0;
   ```

5. **Single `value` Element:**  
   If your annotation has a single element called `value`, you can omit the element name when using the annotation.

   ```java
   public @interface Example {
       String value();
   }
   // Usage:
   @Example("test")
   ```

6. **No Inheritance or Generics:**  
   Annotations cannot extend other annotations and cannot use generic types.

---

#### Example:

```java
public @interface Info {
    String author();
    String date();
    int revision() default 1;
}
```

---

## Types of Annotations

Some common built-in annotation types you’ll see in Java:

- **Compiler Annotations** — Used by the Java compiler
- **Meta-Annotations** — Used to describe your own annotations

---

### Common Built-in Annotations

| Annotation             | Purpose                                                |
| ---------------------- | ------------------------------------------------------ |
| `@Override`            | Checks that a method overrides a parent method         |
| `@Deprecated`          | Marks that something should not be used anymore        |
| `@SuppressWarnings`    | Tells the compiler to skip showing certain warnings    |
| `@FunctionalInterface` | Checks that an interface has only one abstract method  |
| `@SafeVarargs`         | Suppresses unchecked warnings for methods with varargs |

**Example usage:**

```java
@Override
public String toString() {
    return "MyClass";
}

@Deprecated
public void oldMethod() {
    System.out.println("Don't use me!");
}

@SuppressWarnings("unchecked")
public void riskyMethod() {
    // Do something risky here
}

@FunctionalInterface
public interface Printer {
    void print(String msg);
}
```

---

## Meta-Annotations

Meta-annotations are annotations you put on your own annotation definitions to indicate how they should be used.

### `@Target` — Where your annotation can be used

```java
@Target({ElementType.METHOD, ElementType.TYPE})
public @interface MyAnnotation { }
```

Possible targets include classes, methods, fields, parameters, etc.

### `@Retention` — How long the annotation is retained

```java
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation { }
```

- `SOURCE` – Only in the source code, removed by compiler
- `CLASS` – In class file, not available at runtime (default)
- `RUNTIME` – Available at runtime

### `@Documented` — Should appear in Javadoc

```java
@Documented
public @interface MyAnnotation { }
```

### `@Inherited` — Passes from parent class to child class

```java
@Inherited
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation { }
```

### `@Repeatable` — Use multiple times on one element (Java 8+)

```java
@Repeatable(Roles.class)
public @interface Role {
    String value();
}

public @interface Roles {
    Role[] value();
}

@Role("ADMIN")
@Role("USER")
public class Person { }
```

---

## Annotation Lifecycle Overview

```bash
Source Code          .class File               Runtime (JVM)
  @SOURCE        →   Discarded
  @CLASS         →   Stored                →   Not accessible in running program
  @RUNTIME       →   Stored                →   Accessible using Reflection
```
