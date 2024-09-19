### Q. What are relational operators in Kotlin, and how do they work?
Answer: Relational operators compare two values and return a boolean result. In Kotlin, they are:
== for equality
!= for inequality
> for greater than
< for less than
>= for greater than or equal to
<= for less than or equal to Example:

### Q. Explain logical operators in Kotlin and provide examples.
Answer: Logical operators are used to perform logical operations on boolean expressions:
&& (AND) returns true if both expressions are true.
|| (OR) returns true if at least one expression is true.
! (NOT) negates the value of the boolean expression. Example:

### Q. What are the assignment operators in Kotlin?
Answer: Assignment operators are used to assign values to variables. The basic assignment operator is =, but Kotlin also supports compound assignment operators:
+=, -=, *=, /=, %= Example:

### Q. How do increment (++) and decrement (--) operators work in Kotlin?
Answer: The ++ operator increases a variable's value by 1, and -- decreases it by 1. These can be used in both prefix and postfix forms:
Prefix: Increments or decrements before returning the value.
Postfix: Increments or decrements after returning the value.

### Q. How does the == operator differ from the === operator in Kotlin?
Answer: In Kotlin:
== is used for structural equality (compares values). It is equivalent to calling equals() in Java.
=== is used for referential equality (compares if two references point to the same object in memory).

### Q. Can you overload operators in Kotlin? Provide an example

Answer: Yes, Kotlin allows operator overloading by defining functions with special keywords. For example, you can overload the + operator for a custom class by implementing the plus() function. Example:

```Kotlin
class Point(val x: Int, val y: Int) {
    operator fun plus(other: Point): Point {
        return Point(x + other.x, y + other.y)
    }
}
val p1 = Point(2, 3)
val p2 = Point(4, 1)
val p3 = p1 + p2  // Using the overloaded + operator
println("(${p3.x}, ${p3.y})")  // Output: (6, 4)
```

### Q. What is the purpose of the safe call operator (?.) in Kotlin?
Answer: The safe call operator ?. is used to safely access a property or call a method on a nullable object. It returns null if the object is null instead of throwing a NullPointerException. Example:

### Q.  What is the Elvis operator (?:) in Kotlin, and how is it used?

Answer: The Elvis operator ?: is used to provide a default value when the left-hand expression is null. Example:

### Q. How does the range operator `(..)` work in Kotlin?

Answer: The range operator `..` is used to create a range of values. It can be used with numeric types or characters. Example:

### Q. How can you define a reverse range in Kotlin?

Answer: You can define a reverse range using the downTo keyword.

### Q. How is the in operator used in Kotlin, and what does it do?

Answer: The in operator is used to check if a value belongs to a range, collection, or another data structure. It can also be used in conjunction with !in to check if the value is not in the range or collection. Example:

### Q. What is the difference between the is and as operators in Kotlin?

`is` is used to check if an object is of a particular type
`as` is used to cast an object to a specific type (throws a ClassCastException if the casting fails)
`as?` is a safe cast operator, which returns null if the cast is unsuccessful. 