### Q2: What is a data class in Kotlin? ☆☆

**Answer:**
We frequently create classes whose main purpose is to hold data. In Kotlin, this is called a data class and is marked as `data`:

```kotlin
data class User(val name: String, val age: Int)
```

To ensure consistency and meaningful behavior of the generated code, data classes have to fulfill the following requirements:

* The primary constructor needs to have at least one parameter;
* All primary constructor parameters need to be marked as val or var;
* Data classes cannot be abstract, open, sealed or inner;

### Q9: How to create empty constructor for data class in Kotlin? ☆☆☆☆

**Answer:**
If you give **default values to all the fields** - empty constructor is generated automatically by Kotlin.

```kotlin
data class User(var id: Long = -1,
               var uniqueIdentifier: String? = null)
```

and you can simply call:

```kotlin
val user = User()
```

Another option is to declare a secondary constructor that has no parameters:
```kotlin
data class User(var id: Long,
               var uniqueIdentifier: String?){
    constructor() : this(-1, null)
}
```
