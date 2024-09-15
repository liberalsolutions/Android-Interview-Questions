
### Q1: What is a primary constructor in Kotlin? ☆☆

**Answer:**
The **primary constructor** is part of the class header. Unlike Java, you don't need to declare a constructor in the body of the class. Here's an example:

```kotlin
class Person(val firstName: String, var age: Int) {
    // class body
}
```

The main idea is by removing the constructor keyword, our code gets simplified and easy to understand.

### Q2. What is a primary constructor in Kotlin? How is it different from secondary constructors?

A primary constructor is declared in the class header and is part of the class declaration. It can define properties and receive parameters. On the other hand, secondary constructors are additional constructors declared inside the class body. They provide alternative ways to initialize the class. Here's an example:

```Kotlin
class Person(val name: String, val age: Int) {
    constructor(name: String) : this(name, 0) {
        // Secondary constructor
    }
}
```