
### Q1: What is a primary constructor in Kotlin? ☆☆

**Answer:**
The **primary constructor** is part of the class header. Unlike Java, you don't need to declare a constructor in the body of the class. Here's an example:

```kotlin
class Person(val firstName: String, var age: Int) {
    // class body
}
```

The main idea is by removing the constructor keyword, our code gets simplified and easy to understand.