
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

### Q. What is a class in Kotlin, and how does it differ from Java?
A class in Kotlin is a blueprint for creating objects that defines properties, methods, and behaviors. Kotlin classes are similar to Java but with key differences:

In Kotlin, classes are final by default, meaning they cannot be inherited unless marked as open.
Constructors are more concise, and the primary constructor can be declared in the class header.
Kotlin supports data classes that provide automatic implementations of common methods like toString(), equals(), and hashCode().

### Q4. What is the difference between a primary and secondary constructor in Kotlin?

Primary Constructor: A concise way to declare a constructor directly in the class header.

Secondary Constructor: Declared inside the class body and used when additional initialization logic or alternate constructor parameters are needed.

### Q5. Explain the concept of init block in Kotlin. When would you use it?
Answer:
The init block in Kotlin is an initialization block used to perform additional initialization logic in a class. It runs immediately after the primary constructor is called, and multiple init blocks are executed in the order they appear in the class.

You use init when you need to perform some logic during object creation, like setting default values or validating inputs.

class Person(val name: String, var age: Int) {
    init {
        println("Person's name is $name")
    }
}

### Q6. What is the difference between object and class in Kotlin?
class: Defines a blueprint for creating multiple instances (objects) of that class.

object: Used to define a singleton, meaning only one instance of the object exists. An object in Kotlin can also be used to define companion objects, anonymous objects, or utility objects.

object Database {
    val name = "MainDatabase"
    fun connect() {
        println("Connected to $name")
    }
}

### Q7.  What is the difference between open and final classes in Kotlin?
open: A class in Kotlin is final by default, meaning it cannot be inherited. To allow inheritance, the class must be explicitly marked as open.

final: By default, all classes in Kotlin are final, and methods are also final unless explicitly marked open. This prevents unintended inheritance.