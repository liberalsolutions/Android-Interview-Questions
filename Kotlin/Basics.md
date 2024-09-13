### Q9: May you briefly compare Kotlin vs Java? ☆☆☆

**Answer:**
||||
|--- |--- |--- |
|Java vs Kotlin|Java|Kotlin|
|Null Safe|In Java, `NullPointerExceptions` causes huge frustration for developers. It allows users to assign null to any variables but while accessing an object reference having null value raises a null pointer exception which user needs to handle.|In Kotlin, By default, all types of variables are non-null able (i.e. we can’t assign null values to any type of variables/objects). If we try to assign or return null values, Kotlin code will fail during compile-time. If we really want a variable to have a null value, we can declare as follows: `value num: Int? = null`|
|Extension Functions|In Java, If we want to extend the functionality of existing class we need to create a new class and inherit the parent class. So Extension functions are not available in Java|Kotlin provides developers the ability to extend an existing class with new functionality. We can create extend functions by prefixing the name of a class to name of the new function.|
|Coroutines Support|In Java, whenever if we initiate a long-running network I/0 or CPU Intensive operations, the corresponding thread will be blocked. As Android is a single-threaded by default. Java provides the ability to create multiple threads in the background and run but managing them is a complex task.|In Kotlin, We can create multiple threads to run these long-running intensive operations but we have coroutines support, which will suspend execution at a certain point without blocking threads while executing long-running intensive operations.|
|No checked exceptions|In Java, We have checked exceptions support which makes developers declare and catch the exception which ultimately leads to robust code with good error handling.|In Kotlin, we don’t have checked exceptions. So developers don’t need to declare or catch the exceptions, which have advantages and disadvantages.|
|Data classes|In Java, suppose we need to have a class which needs to hold data but nothing else. For this we need to define constructors, variables to store data, getter and setter methods, hashcode(), toString(), and equals() functions|In Kotlin, If we need to have classes which need to hold data we can declare a class with keyword “data” in the class definition then the compiler will take care of all of this work such as creating constructors, getter, setter methods for different fields.|
|Smart casts|In Java, We need to check the type of variables and cast according to our operation.|In Kotlin, smart casts will handle these casting checks with keyword “is-checks” which will check for immutable values and performs implicit casting.|
|Type inference|In Java, we need to specify a type of each variable explicitly while declaring.|In Kotlin, we don’t need to specify the type of each variable explicitly based on assignment it will handle. If we want to specify explicitly we can do.|
|Functional Programming|Java doesn’t have functional programming support till Java 8 but while developing Android applications it supports the only subset of Java 8 features.|Kotlin is a mix of procedural and functional programming language which consists of many useful methods such as lambda, operator overloading, higher-order functions, and lazy evaluation, etc.|


### Q3: Explain advantages of "when" vs "switch" in Kotlin ☆☆☆

**Answer:**


In Java we use switch but in Kotlin, that switch gets converted to **when**. When has a better design. It is more concise and powerful than a traditional **switch**. **when** can be used either as an expression or as a statement.

Some examples of **when** usage:
* Two or more choices
```kotlin
when(number) {
    1 -> println("One")
    2, 3 -> println("Two or Three")
    4 -> println("Four")
    else -> println("Number is not between 1 and 4")
}
```
* "when" without arguments
```kotlin
when {
    number < 1 -> print("Number is less than 1")
    number > 1 -> print("Number is greater than 1")
}
```
* Any type passed in "when"
```kotlin
fun describe(obj: Any): String =
    when (obj) {
      1 -> "One"
      "Hello" -> "Greeting"
      is Long -> "Long"
      !is String -> "Not a string"
      else -> "Unknown"
    }
```
* Smart casting
```kotlin
when (x) {
    is Int -> print("X is integer")
    is String -> print("X is string")
}
```
* Ranges
```kotlin
when(number) {
    1 -> println("One") //statement 1
    2 -> println("Two") //statement 2
    3 -> println("Three") //statement 3
    in 4..8 -> println("Number between 4 and 8") //statement 4
    !in 9..12 -> println("Number not in between 9 and 12") //statement 5
    else -> println("Number is not between 1 and 8") //statement 6
}
```
### Q4: What are the advantages of Kotlin over Java? ☆☆☆

**Answer:**
Basically for me less thinking required to write kotlin equivalent to most java code:

`data class`

*   java: you have to write getters and setters for each thing, you have to write `hashCode` properly (or let IDE auto generate, which you have to do again every time you change the class), `toString` (same problem as `hashcode`) and `equals` (same problem as `hashCode`). or you could use lombok, but that comes with some quirky problems of its own. `record` types are hopefully on the way. \*kotlin: `data class` does it all for you.
    

getter and setter patterns

*   java: rewrite the getter and setter for each variable you use it for
    
*   kotlin: don't have to write getter and setter, and custom getter and setter take a lot less typing in kotlin if you do want to. also delegates exist for identical getters\\setters
    

`abstract` vs `open` classes

*   java: you have to make an abstract class implementation
    
*   kotlin: `open class` lets you make an inheritable class while also being usable itself. nice mix of interface and regular class imo
    

extension functions

*   java: doesnt exist
    
*   kotlin: does exist, makes functions more clear in usage and feels more natural.
    

null

*   java: Anything but primitives can be null at any time.
    
*   kotlin: you get to decide what can and cant be null. allows for nice things like `inline class`
    

singleton

*   java: Memorize singleton pattern
    
*   kotlin: `object` instead of `class`
    

generics

*   java: Theyre alright, nothing fancy
    
*   kotlin: Reified generics (you can access the actual type), `in` and `out` for covariance
    

named parameters

*   java: does not exist, easy to break api back-compatibility if you arent careful.
    
*   kotlin: does exist, easy to preserve api back-compatiblity.
    

primary constructor

*   java: does not have per-se, you still have to define everything inside the class
    
*   kotlin: very nice to be able to quickly write a constructor without any constructor function or extra needless declarations

### Q5: What are some disadvantages of Kotlin? ☆☆☆

**Answer:**
Some think that Kotlin is a mess of extra syntax and keywords. Here are a few keywords which have non-obvious meanings: internal, crossinline, expect, reified, sealed, inner, open. Java has none of these. Kotlin is also amusingly inconsistent in its keywords: a function is is declared with ‘fun’, but an interface is declared with ‘interface’ (not ‘inter’?). Kotlin also doesn’t have checked exceptions. Checked exceptions have become unfashionable, yet many (including me) find them a powerful way to ensure that your code is robust. Finally, Kotlin hides a lot of what goes on. In Java, you can trace through almost every step of program logic. This can be vital for hunting down bugs. In Kotlin, if you define a data class, then getters, setters, equality testing, to string, and hash code are added for you invisibly. This can be a bad idea.

Also according docs, what Java has that Kotlin does not:
* Checked exceptions
* Primitive types that are not classes
* Static members
* Non-private fields
* Wildcard-types
* Ternary-operator a ? b : c


### Q6: What is the difference between "open" and "public" in Kotlin? ☆☆☆

**Answer:**
* The **open** keyword means “open for extension“. The open annotation on a class is the opposite of Java's `final`: _it allows others to inherit from this class_.
* If you do not specify any visibility modifier, **public** is used by default, which means that your declarations will be visible everywhere. **public** is the default if nothing else is specified explicitly.


