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
