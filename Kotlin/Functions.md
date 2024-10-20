## Inline Function

### Q1. What is an inline function in Kotlin?

Answer: An inline function is a function whose body is directly substituted into the places where the function is called, instead of the function being called as usual. This reduces function call overhead and can improve performance, especially when higher-order functions are used.


### Q2. How do you declare an inline function in Kotlin?

Answer: To declare an inline function, use the inline keyword before the function definition:
```Kotlin
inline fun <T> myInlineFunction(block: () -> T): T {
    return block()
}
```

### Q3. What are the benefits of using inline functions in Kotlin?

Answer: Inline functions can:
* Eliminate the overhead of function calls.
* Avoid creating objects for lambda expressions, improving performance.
* Enable non-local returns from lambda expressions passed to inline functions.


### Q4. Explain how inline functions can help in reducing memory allocation when dealing with lambda expressions.

Answer: Normally, when a lambda expression is passed as a parameter to a function, a new object is created for that lambda. However, when a function is marked as inline, the compiler replaces the lambda with the actual code, avoiding the creation of a separate object and reducing memory allocation.



### Q5. What are the limitations of inline functions in Kotlin?

Answer: Some limitations of inline functions include:
You cannot use inline functions with recursive functions, as this would cause an infinite loop during inlining.
Excessive use of inline functions can lead to larger bytecode, possibly impacting performance negatively.
Inline functions cannot use private or protected visibility if they are inside a public or internal class.


### Q6. What are noinline and crossinline in Kotlin, and when would you use them?

Answer:
noinline: If you want to prevent a particular lambda parameter in an inline function from being inlined, you can mark it with the noinline keyword. This is useful when you don't want all lambda expressions passed to an inline function to be inlined..
```Kotlin
inline fun myFunction(inlineLambda: () -> Unit, noinline nonInlineLambda: () -> Unit) {
    inlineLambda()
    nonInlineLambda() // this will not be inlined
}
```

crossinline: When a lambda expression is passed to an inline function and that lambda needs to be inlined, but a non-local return is not allowed, you can use crossinline. This ensures that the lambda cannot return from the outer function.
```Kotlin
inline fun myCrossinlineFunction(crossinline block: () -> Unit) {
    val runnable = Runnable { block() }
    runnable.run() // Non-local return not allowed
}
```

### Q7. What are some real-world use cases for inline functions in Kotlin?

Answer: Inline functions are often used in high-performance applications to reduce the overhead of higher-order functions and lambda expressions. Common use cases include:
Inline extension functions to avoid unnecessary function call overhead.
Inline higher-order functions for collection transformations like map, filter, etc., to improve performance.

### Q8. What are extension functions in Kotlin?

Explain the concept of extension functions and how they are declared.
Example answer: Extension functions allow you to extend the functionality of a class without inheriting or modifying the class. These functions are declared using the fun keyword, followed by the class or type to extend.

### Q9. How do you declare and call an extension function in Kotlin?
Extension functions are declared by specifying the receiver type (the class or type you are extending) followed by the function name. Once declared, they can be called like regular member functions on instances of the receiver type.

### Q10. Can extension functions override member functions in Kotlin?
No, extension functions cannot override member functions. If a class has a member function with the same signature as an extension function, the member function will take precedence, and the extension function will be shadowed.

### Q11. What is the receiver type and receiver object in extension functions?

The receiver type is the type that the extension function is extending (e.g., String, Int, List). The receiver object is the specific instance of that type on which the extension function is called.
```kotlin
fun String.customLength(): Int {
    return this.length * 2 // 'this' refers to the receiver object (instance of String)
}

val result = "Hello".customLength() // Here, "Hello" is the receiver object
```
### Q12. Can you extend a nullable type in Kotlin?

Yes, you can create extension functions for nullable types. In such cases, the receiver object can be null, and you must handle this case inside the function.
```Kotlin
fun String?.isNullOrEmpty(): Boolean {
    return this == null || this.isEmpty()
}

val text: String? = null
println(text.isNullOrEmpty()) // Output: true
```

### Q13.  What is the scope of an extension function?
Extension functions are scoped based on where they are declared. If declared at the top level, they are available throughout the package. If declared inside a class or object, their scope is limited to that class or object.

### Q14. What are the advantages and disadvantages of using extension functions in Kotlin?

Advantages:

* They provide a way to add functionality to existing classes without modifying their source code.
* They help keep code clean and organized by reducing boilerplate.
* They improve readability and usability, especially for third-party libraries.

Disadvantages:

* They can lead to confusion, especially if they have the same name as a member function or if multiple extension functions with the same signature exist.
* They cannot access private members of the class.

### Q15: How are extensions resolved in Kotlin and what doest it mean? ☆☆☆

**Answer:**
Extensions do not actually modify classes they extend. By defining an extension, you do not insert new members into a class, but merely make new functions callable with the dot-notation on variables of this type.

The extension functions dispatched **statically**. That means the extension function which will be called is determined by the type of the expression on which the function is invoked, not by the type of the result of evaluating that expression at runtime. In short, they are not virtual by receiver type.

Consider:
```kotlin
open class BaseClass

class DerivedClass : BaseClass()

fun BaseClass.someMethod(){
    print("BaseClass.someMethod")
}

fun DerivedClass.someMethod(){
    print("DerivedClass.someMethod")
}

fun printMessage(base : BaseClass){
    base.someMethod()
}

printMessage(DerivedClass())
```

This will print 

```sh
BaseClass.someMethod
```

because the extension function being called depends only on the declared type of the parameter `base` in `printMessage` method, which is the `BaseClass` class. This is different from runtime polymorphism as here it is resolved **statically** but not at the runtime.

### Q16. What is a lambda function in Kotlin?
Ans: A lambda function in Kotlin is an anonymous function (a function without a name) that can be treated as a value. It can be passed as an argument to other functions, stored in variables, or returned from functions. 
```kotlin
val sum = { a: Int, b: Int -> a + b }
println(sum(3, 4))  // Output: 7
```
### Q17. What is the implicit it in Kotlin lambda expressions?
If a lambda function has only one parameter, Kotlin allows you to omit the parameter declaration and use the implicit keyword it to refer to the parameter. This helps to make the lambda more concise.
```Kotlin
val square = { it * it }
println(square(5))  // Output: 25
```

### Q18. What is the purpose of the inline keyword in the context of lambdas?
In Kotlin, the inline keyword is used to reduce the overhead caused by higher-order functions. When a function is marked as inline, the compiler inlines the function's body, meaning that the function call is replaced by the actual code during compilation. This can improve performance by avoiding the creation of additional function objects and stack frames.
```Kotlin
inline fun performOperation(x: Int, operation: (Int) -> Int): Int {
    return operation(x)
}

fun main() {
    val result = performOperation(4) { it * 2 }
    println(result)  // Output: 8
}
```

### Q . What are higher-order functions in Kotlin? Provide an example.
Higher-order functions are functions that can accept other functions as parameters or return functions as results. They allow for a more functional programming style in Kotlin. Here’s an example:
```Kotlin
fun performOperation(x: Int, y: Int, operation: (Int, Int) -> Int): Int {
    return operation(x, y)
}
```

```Kotlin
val sum: (Int, Int) -> Int = { a, b -> a + b }
val result = performOperation(5, 3, sum) // result will be 8
```

### Q. What are Kotlin standard library higher-order functions like map, filter, reduce, and flatMap?

* `map`: Transforms each element of a collection using a lambda and returns a new collection.
* `filter`: Returns a collection containing only the elements that satisfy the given predicate.
* `reduce`: Accumulates the elements of a collection into a single value using the provided operation.
* `flatMap`: Maps each element of a collection to another collection and then flattens the result.
```Kotlin
val numbers = listOf(1, 2, 3, 4)

// map example
val doubled = numbers.map { it * 2 } 
println(doubled)  // Output: [2, 4, 6, 8]

// filter example
val evenNumbers = numbers.filter { it % 2 == 0 }
println(evenNumbers)  // Output: [2, 4]

// reduce example
val sum = numbers.reduce { acc, number -> acc + number }
println(sum)  // Output: 10
```

### Q. What is the difference between map and flatMap in Kotlin?

* `map`: Transforms each element into another object, resulting in a list of transformed elements.
* `flatMap`: Transforms each element into another collection and then flattens all the resulting collections into a single list.
```Kotlin
val numbers = listOf(1, 2, 3)

// map
val mapped = numbers.map { listOf(it, it + 1) }
println(mapped)  // Output: [[1, 2], [2, 3], [3, 4]]

// flatMap
val flatMapped = numbers.flatMap { listOf(it, it + 1) }
println(flatMapped)  // Output: [1, 2, 2, 3, 3, 4]
```

### Q. What is the difference between a lambda expression and an anonymous function in Kotlin?



### Q. What is a higher-order function with receiver in Kotlin.