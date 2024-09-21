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
Eliminate the overhead of function calls.
Avoid creating objects for lambda expressions, improving performance.
Enable non-local returns from lambda expressions passed to inline functions.


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

### Q4: How are extensions resolved in Kotlin and what doest it mean? ☆☆☆

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

### Q. What is the difference between a lambda expression and an anonymous function in Kotlin?


### Q. What is a higher-order function with receiver in Kotlin.