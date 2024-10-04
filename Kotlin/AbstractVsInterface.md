What is the difference between an Abstract class and an Interface?

Abstract classes and interfaces serve different purposes and have distinct capabilities. While there is some overlap in what they can do, there are key differences between the two.

1. Constructor: Abstract classes can have constructors, whereas interfaces cannot. Abstract classes can be used to define common constructor logic for their subclasses, which is not possible with interfaces.

2. Fields: Abstract classes can have fields (instance variables), including private ones, whereas interfaces can only declare constants (public static final fields).

3. Method Implementation: Abstract classes can provide concrete (i.e., implemented) methods in addition to abstract methods, while interfaces can only declare method signatures (abstract methods) but cannot provide implementations.

4. Multiple Inheritance: In Java, a class can extend only one abstract class, but it can implement multiple interfaces. This means interfaces are more flexible when it comes to multiple inheritance.

5. Default Methods: Java introduced default methods in interfaces (since Java 8) to provide method implementations in interfaces. Abstract classes still offer more flexibility in terms of method implementation.

6. Access Modifiers: Interface methods are by default public and abstract (no need to specify the “public” or “abstract” modifiers), while abstract class methods can have various access modifiers, including private and protected.

7. Usage: Abstract classes are typically used when you want to provide a common base class with some shared behavior and leave room for customization by subclasses. Interfaces are used when you want to define a contract that multiple classes can adhere to, regardless of their inheritance hierarchy.