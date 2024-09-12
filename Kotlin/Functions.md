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