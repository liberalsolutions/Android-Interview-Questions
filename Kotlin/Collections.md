### Q1: How to initialize an array in Kotlin with values? ☆☆

**Details:**
In Java an array can be initialized such as:

```java
 int numbers[] = new int[] {10, 20, 30, 40, 50}
 val simpleArray = arrayOf(1, 2, 3)
```

### Q.2 How does Kotlin's array initialization look like?

**Answer:**
```kotlin
val numbers: Array  = arrayOf(10, 20, 30, 40, 50)
```


### Q3: What is basic difference between fold and reduce in Kotlin? When to use which? ☆☆

**Answer:**
* `fold` takes an initial value, and the first invocation of the lambda you pass to it will receive that initial value and the first element of the collection as parameters.

 ```kotlin 
 listOf(1, 2, 3).fold(0) { sum, element -> sum + element }
 ```
 The first call to the lambda will be with parameters `0` and `1`.

 Having the ability to pass in an initial value is useful _if you have to provide some sort of default value or parameter for your operation_.

* `reduce` doesn't take an initial value, but instead starts with the first element of the collection as the accumulator (called `sum` in the following example)

 ```kotlin
 listOf(1, 2, 3).reduce { sum, element -> sum + element }
 ```

 The first call to the lambda here will be with parameters `1` and `2`.


 ### Q15: What is the idiomatic way to remove duplicate strings from array? ☆☆

**Details:**
How to remove duplicates from an `Array<String?>` in Kotlin?

**Answer:**
Use the `distinct` extension function:

```kotlin
val a = arrayOf("a", "a", "b", "c", "c")
val b = a.distinct() // ["a", "b", "c"]
```

You can also use:
* `toSet`, `toMutableSet`
* `toHashSet` - if you don't need the original ordering to be preserved

These functions produce a `Set` instead of a `List` and should be a little bit more efficient than distinct.

### Q8: How to convert List to Map in Kotlin? ☆☆☆

**Answer:**
You have two choices:

* The first and most performant is to use `associateBy` function that takes two lambdas for generating the key and value, and inlines the creation of the map:

 ```kotlin
val map = friends.associateBy({it.facebookId}, {it.points})
```

* The second, less performant, is to use the standard `map` function to create a list of `Pair` which can be used by `toMap` to generate the final map:

 ```kotlin
val map = friends.map { it.facebookId to it.points }.toMap()
```
### Q10: What is the difference between List and Array types? ☆☆☆

**Answer:**
The major difference from usage side is that `Arrays` have a fixed size while `(Mutable)List `can adjust their size dynamically. Moreover `Array` is mutable whereas `List` is not.

Furthermore `kotlin.collections.List` is an interface implemented among others by `java.util.ArrayList`. It's also extended by `kotlin.collections.MutableList `to be used when a collections that allows for item modification is needed.

On the jvm level `Array` is represented by arrays. `List` on the other hand is represented by `java.util.List` since there are no immutable collections equivalents available in Java.

### Q14: May you use IntArray and an Array<Int> is in Kotlin interchangeably? ☆☆☆

**Answer:**
`Array<Int>` is an `Integer[]` under the hood, while `IntArray` is an `int[]`. 

This means that when you put an `Int` in an `Array<Int>`, it will always be boxed (specifically, with an `Integer.valueOf()` call). In the case of `IntArray`, no boxing will occur, because it translates to a Java primitive array.

So **no**, we can't use them interchangeably.