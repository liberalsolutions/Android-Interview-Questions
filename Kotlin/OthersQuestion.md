### Q1: Explain what is wrong with that code? ☆☆☆

**Details:**
Why is this code wrong?

```kotlin
class Student (var name: String) {
    init() {
        println("Student has got a name as $name")
    }

    constructor(sectionName: String, var id: Int) this(sectionName) {
    }
}
```

**Answer:**
The property of the class can’t be declared inside the secondary constructor.. This will give an error because here we are declaring a property `id` of the class in the secondary constructor, which is not allowed.

If you want to use some property inside the secondary constructor, then declare the property inside the class and use it in the **secondary constructor**:

```kotlin
class Student (var name: String) {

    var id: Int = -1
    init() {
        println("Student has got a name as $name")
    }
    
    constructor(secname: String, id: Int) this(secname) {
        this.id = id
    }
}
```

### 2: What will be result of the following code execution? ☆☆☆

**Details:**
What will be the output?
```kotlin
val aVar by lazy {
    println("I am computing this value")
    "Hola"
}
fun main(args: Array<String>) {
    println(aVar)
    println(aVar)
}
```

**Answer:**
For `lazy` the first time you access the Lazy property, the initialisation (`lazy()` function invocation) takes place. The second time, this value is remembered and returned:

```sh
I am computing this value
Hola
Hola
```

### Q15: Rewrite this code in Kotlin ☆☆☆

**Details:**
Can you rewrite this Java code in Kotlin?
```java
public class Singleton {
    private static Singleton instance = null;
    private Singleton(){
    }
    private synchronized static void createInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
    }
    public static Singleton getInstance() {
        if (instance == null) createInstance();
        return instance;
    }

```

**Answer:**
Using Kotlin:
```kotlin
object Singleton
```


### Q18: What is the purpose of Unit-returning in functions? Why is VALUE there? What is this VALUE? ☆☆☆

**Details:**
Explain what is the purpose of Unit-returning in functions? Why is VALUE there? What is this VALUE?
```kotlin
fun printHello(name : String?) : Unit { 
   if (name != null) 
     print("Hello, $name!") 
   else 
     print("Hi there!") 
   // We don't need to write 'return Unit.VALUE' or 'return', although we could 
}
```

**Answer:**
The purpose is the same as C's or Java's `void`. Only Unit is a proper type, so it can be passed as a generic argument etc.

1. Why we don't call it "Void": because the word "void" means "nothing", and there's another type, `Nothing`, that means just "no value at all", i.e. the computation did not complete normally (looped forever or threw an exception). We could not afford the clash of meanings.

2. Why Unit has a value (i.e. is not the same as Nothing): because generic code can work smoothly then. If you pass Unit for a generic parameter T, the code written for any T will expect an object, and there must be an object, the sole value of Unit.

3. How to access that value of Unit: since it's a singleton object, just say `Unit`

4. `UNIT` actually contains valuable information, it basically just means "DONE". It just returns the information to the caller, that the method has been finished. 


> Explain the concept of generics in Kotlin. How are generics used in Android development?