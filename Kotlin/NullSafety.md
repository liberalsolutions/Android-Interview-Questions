### Q1: Explain the Null safety in Kotlin ☆☆☆

**Answer:**
Kotlin's type system is aimed at eliminating the danger of null references from code, also known as the The Billion Dollar Mistake.

One of the most common pitfalls in many programming languages, including Java, is that accessing a member of a null reference will result in a null reference exception. In Java this would be the equivalent of a `NullPointerException` or NPE for short.

In Kotlin, the type system distinguishes between references that can hold `null` (nullable references) and those that can not (`non-null` references). For example, a regular variable of type String can not hold null:

```kotlin
var a: String = "abc"
a = null // compilation error
```
To allow nulls, we can declare a variable as nullable string, written `String?`:
```kotlin
var b: String? = "abc"
b = null // ok
print(b)
```

### Q2. What is the purpose of the safe call operator (?.) in Kotlin?
Answer: The safe call operator ?. is used to safely access a property or call a method on a nullable object. It returns null if the object is null instead of throwing a NullPointerException. Example:

### Q3: What is the Kotlin double-bang (!!) operator? ☆☆☆

**Answer:**
The **not-null assertion operator !!** converts any value to a non-null type and throws a `KotlinNullPointerException` exception if the value is null.

Consider:
```kotlin
fun main(args: Array<String>) {
    var email: String?
    email = null
    println(email!!)
}
```
This operator should be used in cases where the developer is guaranteeing – it allows you to be 100% sure that its value is not null. 

### Q4: When would you use Elvis operator in Kotlin? ☆☆☆

**Answer:**
The Elvis operator is part of many programming languages, e.g. Kotlin but also Groovy or C#. The Elvis operator is the ternary operator with its second operand omitted.

```kotlin
x ?: y // yields `x` if `x` is not null, `y` otherwise.
```
If `x` isn't null, then it will be returned. If it is null, then the `y` will be returned. 

### Q5: What is the idiomatic way to deal with nullable values, referencing or converting them? ☆☆☆

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

### Q6. How do you declare a nullable type in Kotlin?
Answer: You declare a nullable type by appending ? to the type declaration

```Kotlin
var name: String? = null
```


### Q7. What is the purpose of the safe call operator (?.), and how is it used?

Answer: The safe call operator (?.) is used to safely access a property or method on a nullable object. If the object is null, it returns null instead of throwing a NullPointerException. Example:

```Kotlin
val name: String? = null
val length = name?.length  // Safely returns null if 'name' is null
println(length)  // Output: null
```

### Q8. What is the safe cast operator (as?) in Kotlin, and how is it different from regular type casting?

The safe cast operator (as?) attempts to cast a value to a type. If the cast fails, it returns null instead of throwing a ClassCastException. Example:

### Q9: What is the purpose of the let function in Kotlin, and how is it used with null safety?
Answer: The let function is used to execute a block of code only if the variable is non-null. It’s commonly used with nullable types for safe code execution. Example:
```Kotlin
val name: String? = "Kotlin"
name?.let {
    println("Name length: ${it.length}")  // Only runs if 'name' is non-null
}
```

### Q10. How do you handle nullability in Kotlin collections (e.g., list, map)?
Collections in Kotlin can either allow null values or be non-nullable. You can define a nullable collection element by using T? for the element type. Example:

```Kotlin

```

### Q11. What is a smart cast in Kotlin, and how does it relate to null safety?

Smart cast automatically casts a variable to a non-nullable type when Kotlin can be sure that the variable isn't null. This happens typically after a null check (if or when condition). Example:

```Kotlin
val name: String? = "Kotlin"
if (name != null) {
    println(name.length)  // Smart cast: no need for name?.length
}
```

### Q12. How does Kotlin handle null safety for function parameters?

In Kotlin, you can explicitly declare function parameters as nullable by using the ? symbol. The function should handle the possible null cases appropriately, either using safe calls, the Elvis operator, or null checks. Example:

```Kotlin
fun printLength(str: String?) {
    val length = str?.length ?: "String is null"
    println(length)
}
```

