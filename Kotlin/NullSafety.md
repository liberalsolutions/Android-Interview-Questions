### Q3: Explain the Null safety in Kotlin ☆☆☆

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

### Q17: What is the Kotlin double-bang (!!) operator? ☆☆☆

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

### Q19: When would you use Elvis operator in Kotlin? ☆☆☆

**Answer:**
The Elvis operator is part of many programming languages, e.g. Kotlin but also Groovy or C#. The Elvis operator is the ternary operator with its second operand omitted.

```kotlin
x ?: y // yields `x` if `x` is not null, `y` otherwise.
```
If `x` isn't null, then it will be returned. If it is null, then the `y` will be returned. 