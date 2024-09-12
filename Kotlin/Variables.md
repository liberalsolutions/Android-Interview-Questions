### Q12: What is the difference between var and val in Kotlin? ☆☆

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

### Q17: Where should I use var and where val? ☆☆

**Answer:**
Use **var** where value is changing _frequently_. For example while getting location of android device:

```kotlin
var integerVariable : Int? = null
```

Use **val** where there is _no change_ in value in whole class. For example you want set textview or button's text programmatically.

```kotlin
val stringVariables : String = "Button's Constant or final Text"
```

### Q7: What is the difference between “const” and “val”? ☆☆☆

**Answer:**
`const`s are compile time constants. Meaning that their value has to be assigned during compile time, unlike `val`s, where it can be done at runtime.


This means, that `const`s can never be assigned to a function or any class constructor, but only to a `String` or primitive.

For example:

```kotlin
const val foo = complexFunctionCall()   //Not okay
val fooVal = complexFunctionCall()      //Okay
 
const val bar = "Hello world"           //Also okay
```

### Q9: What is the idiomatic way to deal with nullable values, referencing or converting them? ☆☆☆

**Details:**
If I have a nullable type `Xyz?`, I want to reference it or convert it to a non-nullable type `Xyz`. What is the idiomatic way of doing so in Kotlin?

**Answer:**
You have several options:

```kotlin
val something: Xyz? = createPossiblyNullXyz()

// access it as non-null asserting that with a sure call
// throws an exception if the value is null
val result1 = something!!.foo()

// access it only if it is not null using safe operator, 
// returning null otherwise
val result2 = something?.foo()

// access it only if it is not null using safe operator, 
// otherwise a default value using the elvis operator
val result3 = something?.foo() ?: differentValue

// null check it with `if` expression and then use the value, 
// similar to result3 but for more complex cases harder to do in one expression
val result4 = if (something != null) {
                   something.foo() 
              } else { 
                   ...
                   differentValue 
              }

// null check it with `if` statement doing a different action
if (something != null) { 
    something.foo() 
} else { 
    someOtherAction() 
}
```

### Q13: How to correctly concatenate a String in Kotlin? ☆☆

**Answer:**
In Kotlin, you can concatenate 
1. using string interpolation / templates
 ```kotlin
val a = "Hello"
val b = "World"
val c = "$a $b"
 ```
2. using the + / `plus()` operator
 ```kotlin
 val a = "Hello"
 val b = "World" 
 val c = a + b   // same as calling operator function a.plus(b)
 val c = a.plus(b)
 
 print(c)
 ```
3. using the `StringBuilder`
 ```kotlin
 val a = "Hello"
 val b = "World"
 
 val sb = StringBuilder()
 sb.append(a).append(b)
 val c = sb.toString()
 
 print(c)
 ```


 ### Q11: val mutableList vs var immutableList. When to use which in Kotlin? ☆☆☆

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


### Q13: How is it recommended to create constants in Kotlin? ☆☆☆

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

