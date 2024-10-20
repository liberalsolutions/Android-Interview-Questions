
### Q1: What is Lateinit in Kotlin and when would you use it? ☆☆☆

**Answer:**
**lateinit** means _late initialization_. If you do not want to initialize a variable in the constructor instead you want to initialize it later on and if you can guarantee the initialization before using it, then declare that variable with lateinit keyword. It will not allocate memory until initialized. You cannot use lateinit for primitive type properties like Int, Long etc.

```kotlin
lateinit var test: String

fun doSomething() {
    test = "Some value"
    println("Length of string is "+test.length)
    test = "change value"
}
```

### Q2: Explain lazy initialization in Kotlin ☆☆☆

**Answer:**
**lazy** means lazy initialization. Your variable will not be initialized unless you use that variable in your code. It will be initialized only once after that we always use the same value.

`lazy()` is a function that takes a lambda and returns an instance of lazy which can serve as a delegate for implementing a lazy property: the first call to `get()` executes the lambda passed to `lazy()` and remembers the result, subsequent calls to `get() `simply return the remembered result.

```kotlin
val test: String by lazy {
    val testString = "some value"
    testString // it has to be return
}
```
```Kotlin
val myLazyString: String by lazy { "Hello" }
```
There are a handful of use cases where this is extremely helpful, for example:

* Android: variables that get initialized in lifecycle methods;
* Using Dagger for DI: injected class variables are initialized outside and independently from the constructor;
* Setup for unit tests: test environment variables are initialized in a `@Before` - annotated method;
* Spring Boot annotations (eg. `@Autowired`).

### Q8: When to use lateinit over lazy initialization in Kotlin? ☆☆☆

**Answer:**


There are some simple rules to determined if you should use one or the other for properties initialisation:
* If properties are mutable (i.e. might change at a later stage) use **lateInit**
* If properties are set externally (e.g. need to pass in some external variable to set it), use **lateinit**. There’s still workaround to use lazy but not as direct.
* If they are only meant to initialized once and shared by all, and it’s more internally set (dependent on variable internal to the class), then use **lazy**. Tactically, you could still use lateinit, but using** lazy** would better encapsulate your initialization code.


Also compare:

|||
|--- |--- |
|**lateinit** var|by **lazy**|
|Can be initialized from anywhere the object seen from.|Can only be initialized from the initializer lambda.|
|Multiple initialization possible.|Only initialize single time.|
|Non-thread safe. It’s up to user to initialize correctly in a multi-threaded environment.|Thread-safety by default and guarntees that the initializer is invoked by once.|
|Can only be used for var.|Can only be used for val.|
|Not eligible for nonnull properties.|Not eligible for nonnull properties.|
|An isInitialized method added to check whether the value has been initialized before.|Property never able to un-initialized.|
|Not allowed on properties of primitive types.|Allowed on properties of primitive types.|
