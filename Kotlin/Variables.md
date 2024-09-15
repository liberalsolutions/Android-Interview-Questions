### Q1: What is the difference between var and val in Kotlin? ☆☆

**Answer:**
* **var** is like `general` variable and it's known as a _mutable_ variable in kotlin and can be assigned multiple times.

* **val** is like `Final` variable and it's known as _immutable_ in Kotlin and can be initialized only single time.

```sh
+----------------+-----------------------------+---------------------------+
|                |             val             |            var            |
+----------------+-----------------------------+---------------------------+
| Reference type | Immutable(once initialized  | Mutable(can able to change|
|                | can't be reassigned)        | value)                    |
+----------------+-----------------------------+---------------------------+
| Example        | val n = 20                  | var n = 20                |
+----------------+-----------------------------+---------------------------+
| In Java        | final int n = 20;           | int n = 20;               |
+----------------+-----------------------------+---------------------------+
```

### Q2: Where should I use var and where val? ☆☆

**Answer:**
Use **var** where value is changing _frequently_. For example while getting location of android device:

```kotlin
var integerVariable : Int? = null
```

Use **val** where there is _no change_ in value in whole class. For example you want set textview or button's text programmatically.

```kotlin
val stringVariables : String = "Button's Constant or final Text"
```

### Q3: What is the difference between “const” and “val”? ☆☆☆

**Answer:**
`const`s are compile time constants. Meaning that their value has to be assigned during compile time, unlike `val`s, where it can be done at runtime.


This means, that `const`s can never be assigned to a function or any class constructor, but only to a `String` or primitive.

For example:

```kotlin
const val foo = complexFunctionCall()   //Not okay
val fooVal = complexFunctionCall()      //Okay
 
const val bar = "Hello world"           //Also okay
```

 ### Q4: val mutableList vs var immutableList. When to use which in Kotlin? ☆☆☆

**Answer:**
Mutable and immutable list increase the design clarity of the model. <br>
This is to force developer to think and clarify the purpose of collection.

 1. If the collection will change as part of design, use mutable collection
 2. If model is meant only for viewing, use immutable list

Purpose of `val` and `var` is different from immutable and mutable list. <br>
***`val`*** and ***`var`*** keyword talk about the how a value/reference of a variable should be treated.

 - ***`var`*** - value/reference assigned to a variable can be changed at any point of time.
 - ***`val`*** - value/reference can be assigned only once to a variable and can't be changed later point in the execution.

There are several reasons why immutable objects are often preferable:

* They encourage functional programming, where state is not mutated, but passed on to the next function which creates a new state based on it. This is very well visible in the Kotlin collection methods such as map, filter, reduce, etc.
* A program without side effects is often easier to understand and debug (you can be sure that the value of an object will always be the one at its definition).
* In multithreaded programs, immutable resources cannot cause race conditions, as no write access is involved.

You have also some disadvantages:

* Copying entire collections just to add/remove a single element is computationally expensive.
* In some cases, immutability can make the code more complex, when you tediously need to change single fields. In Kotlin, data classes come with a built-in copy() method where you can copy an instance, while providing new values for only some of the fields.


### Q5: How is it recommended to create constants in Kotlin? ☆☆☆

**Answer:**
In Kotlin, if you want to create the local constants which are supposed to be used with in the class then you can create it like below:

```kotlin
val MY_CONSTANT_1 = "Constants1"
// or 
const val MY_CONSTANT_2 = "Constants2"
```

Like `val`, variables defined with the `const` keyword are immutable. The difference here is that **const is used for variables that are known at compile-time**.

Also avoid using companion objects. Behind the hood, getter and setter instance methods are created for the fields to be accessible. Calling instance methods is technically more expensive than calling static methods. Instead define the constants in `object`:

```kotlin
object DbConstants {
        const val TABLE_USER_ATTRIBUTE_EMPID = "_id"
        const val TABLE_USER_ATTRIBUTE_DATA = "data"
}
```

### Q. Explain the concept of `type inference` in Kotlin. How does it help in reducing code verbosity?

Answer: Type inference in Kotlin allows the compiler to automatically determine the type of a variable or expression based on its context. It eliminates the need for explicitly declaring the type, reducing code verbosity. Here's an example:
```Kotlin
val number = 42 // The compiler infers the type as Int
val list = listOf(1, 2, 3) // The compiler infers the type as List<Int>
```

### Q. What are the visibility modifiers available in Kotlin? Explain each one briefly.

Kotlin provides four visibility modifiers:

* private: Visible only within the same file.
* protected: Visible within the same file and subclasses.
* internal: Visible within the same module.
* public: Visible everywhere (default if no modifier is specified).


### Q.  What is the purpose of the operator modifier in Kotlin?

The operator modifier in Kotlin is used to overload or define custom behavior for operators. It allows you to provide custom implementations for built-in operators such as +, -, *, /, ==, !=, etc. By using the operator modifier, you can define how your objects should behave when operated upon with specific operators. Here's an example:
```Kotlin
data class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }
}

fun main() {
    val p1 = Point(1, 2)
    val p2 = Point(3, 4)
    val sum = p1 + p2
    println(sum) // Output: Point(x=4, y=6)
}
```