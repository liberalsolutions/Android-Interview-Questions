> Abstract
> Interface


### Q. What is the key difference between an abstract class and an interface in Kotlin?
Abstract class: Can contain both abstract methods (without a body) and concrete methods (with implementation). It is designed to be inherited by a single subclass (single inheritance).
Interface: Can only define abstract methods (but Kotlin allows methods with default implementations). It can be implemented by multiple classes, enabling multiple inheritance.

### Q. How do you declare an abstract class and an interface in Kotlin?

```java
abstract class Animal {
    abstract fun makeSound()
}
```
```java
interface Sound {
    fun makeSound()
}
```

### Q. Can you implement multiple interfaces and extend an abstract class simultaneously?
Yes. A class in Kotlin can extend a single abstract class and implement multiple interfaces
```java
abstract class Animal {
    abstract fun makeSound()
}

interface Flyer {
    fun fly()
}

class Bird : Animal(), Flyer {
    override fun makeSound() { println("Chirp") }
    override fun fly() { println("Flying") }
}
```

### Q. Can an interface provide method implementations in Kotlin?
Yes, in Kotlin, interfaces can have default method implementations
```Java
interface Flyer {
    fun fly() {
        println("Flying")
    }
}
```

### Q. Can an abstract class implement an interface in Kotlin?

Yes, an abstract class can implement an interface and provide implementations for the interface’s methods (or leave them abstract).
```java
interface Flyer {
    fun fly()
}

abstract class Bird : Flyer {
    override fun fly() {
        println("Bird is flying")
    }
}
```

### Q. Can you create an instance of an abstract class or an interface?
No, you cannot instantiate an abstract class or an interface directly. They must be inherited by a concrete class.

### Q.  Can an interface inherit from another interface in Kotlin?
Yes, an interface can inherit from one or more other interfaces.
```java
interface Animal {
    fun makeSound()
}

interface Flyer : Animal {
    fun fly()
}
```