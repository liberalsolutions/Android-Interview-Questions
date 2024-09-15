# Enums in Kotlin: Kotlin Interview Questions & Answers

---

### 1. What is an Enum in Kotlin?

An enum class in Kotlin is a special type that represents a set of constant values.

```kotlin
enum class Color {
    RED, GREEN, BLUE
}
```
### 2. Can enums have properties and methods?

Yes, enums can have properties and methods.

```kotlin
enum class Direction(val degrees: Int) {
    NORTH(0),
    EAST(90),
    SOUTH(180),
    WEST(270);

    fun rotate(degrees: Int): Direction {
        val newDegrees = (this.degrees + degrees) % 360
        return values().first { it.degrees == newDegrees }
    }
}
```

### 4. How are enum constants accessed in Kotlin?
Enum constants are accessed using their names.

```kotlin
val color: Color = Color.RED
```
### 5. Can enums have custom properties for each constant?
Yes, enums can have custom properties for each constant, as shown in the previous example.


### 6. What is the purpose of the `values()` function in enums?
The `values()` function returns an array of enum constants, allowing you to iterate over them.


### 7. How can you use enums in `when` expressions?
Enums are often used in `when` expressions for exhaustive checks.

```kotlin
when (direction) {
    Direction.NORTH -> println("Heading North")
    Direction.EAST -> println("Heading East")
    Direction.SOUTH -> println("Heading South")
    Direction.WEST -> println("Heading West")
}
```

### 8. Can enums implement interfaces in Kotlin?
Yes, enums can implement interfaces.

```kotlin
interface Printable {
    fun printInfo()
}

enum class Weekday : Printable {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY;
    
    override fun printInfo() {
        println("It's a weekday.")
    }
}
```

### 9. What is the use of the `valueOf()` function in enums?
The `valueOf()` function is used to obtain an enum constant by its name.

### 10. How do you define custom methods for individual enum constants?
Custom methods are defined inside the enum class, as shown in a previous example.


### 11. Can enums have constructor parameters?
Yes, enums can have constructor parameters for each constant.

```kotlin
enum class Planet(val mass: Double, val radius: Double) {
    EARTH(5.97e24, 6371.0),
    MARS(6.39e23, 3389.5),
    VENUS(4.87e24, 6051.8);
}
```

### 12. How do you get the `ordinal` value of an enum constant?
The `ordinal` value represents the `position` of an enum constant in the declaration order.

```kotlin
val ordinalValue: Int = Color.RED.ordinal
```

### 13. What is the purpose of the `name` property in enums?
The name property returns the `name` of the enum constant as a string.

```kotlin
val name: String = Color.RED.name
```
### 14. How can you use enums in a `when` expression with multiple conditions?
Enums can be used in a `when` expression with multiple conditions.

```kotlin
when {
    direction in setOf(Direction.NORTH, Direction.EAST) -> println("Heading Northeast")
    direction == Direction.SOUTH -> println("Heading South")
    else -> println("Heading in another direction")
}
```

### 15. What is the significance of the `compareTo()` function in enums?
The `compareTo()` function is used to compare the ordinal values of two enum constants.

```kotlin
println(Direction.WEST.name.compareTo(Direction.EAST.name)) // Return 18 as W is ahed of E
println(Direction.WEST.compareTo(Direction.EAST)) // Retun 2 as it West Comes after East in the order
```
### 16. How can you iterate over the constants of an enum using a loop?
Enums can be iterated using a loop or using the values() function.

```kotlin
for (day in Weekday.values()) {
    println(day)
}
```

### 17. How do you use enums for the singleton pattern in Kotlin?
Enums can be used for implementing a singleton pattern in Kotlin.

```kotlin
enum class Singleton {
    INSTANCE;
    
    fun performOperation() {
        println("Performing operation")
    }
}
```

### 18. What is the difference between an enum class and a regular class with constants?
Enum classes provide a more structured way to represent a fixed set of constants, and they can have behavior.


### 19. How can you use enum classes in a sealed class hierarchy?
### 20. How can you compare enum values in Kotlin?
```kotlin
val direction1 = Direction.NORTH
val direction2 = Direction.EAST

println(direction1 == direction2) // Output: false
println(direction1 === direction2) // Output: false
```
