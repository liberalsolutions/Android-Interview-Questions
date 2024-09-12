### Q10: What are coroutines in Kotlin? ☆☆☆

**Answer:**
Unlike many other languages with similar capabilities, async and await are not keywords in Kotlin and are not even part of its standard library. 

`kotlinx.coroutines` is a rich library for coroutines developed by JetBrains. It contains a number of high-level coroutine-enabled primitives, including `launch`, `async` and others. Kotlin Coroutines give you an API to write your asynchronous code sequentially. 

The documentation says Kotlin Coroutines are like lightweight threads. They are lightweight because creating coroutines doesn’t allocate new threads. Instead, they use predefined thread pools, and smart scheduling. Scheduling is the process of determining which piece of work you will execute next.

Additionally, coroutines can be **suspended** and **resumed** mid-execution. This means you can have a long-running task, which you can execute little-by-little. You can pause it any number of times, and resume it when you’re ready again. 

### Q20: What is the difference between suspending vs. blocking? ☆☆☆

**Answer:**
* A **blocking** call to a function means that a call to any other function, from the same thread, will halt the parent’s execution. Following up, this means that if you make a blocking call on the main thread’s execution, you effectively freeze the UI. Until that blocking calls finishes, the user will see a static screen, which is not a good thing.

* **Suspending** doesn’t necessarily block your parent function’s execution. If you call a suspending function in some thread, you can easily push that function to a different thread. In case it is a heavy operation, it won’t block the main thread. If the suspending function has to suspend, it will simply pause its execution. This way you free up its thread for other work. Once it’s done suspending, it will get the next free thread from the pool, to finish its work.

### Q2: What is suspending function in Kotlin? ☆☆☆

**Answer:**
A **suspending function** is just a regular Kotlin function with an additional suspend modifier which indicates that the function can suspend the execution of a coroutine without blocking the current thread. This means that the code you are looking at might stop executing at the moment it calls a suspending function, and will resume at some later time. However, it doesn’t say anything about what the current thread will do in the meantime.

Suspending functions can invoke any other regular functions, but to actually suspend the execution, it has to be another suspending function.A suspending function cannot be invoked from a regular function, therefore several so-called coroutine builders are provided, which allow calling a suspending function from a regular non-suspending scope like `launch`, `async`, `runBlocking`.

### Q4: What is Coroutine Scope and how is that different from Coroutine Context? ☆☆☆☆

**Answer:**
* Coroutines always execute in some context represented by a value of the **CoroutineContext** type, defined in the Kotlin standard library. The coroutine context is a set of various elements. The main elements are the **Job** of the coroutine.

* **CoroutineScope** has no data on its own, it just holds a **CoroutineContext**. Its key role is as the implicit receiver of the block you pass to `launch`, `async` etc.

 ```kotlin
runBlocking {
    val scope0 = this
    // scope0 is the top-level coroutine scope.
    scope0.launch {
        val scope1 = this
        // scope1 inherits its context from scope0. It replaces the Job field
        // with its own job, which is a child of the job in scope0.
        // It retains the Dispatcher field so the launched coroutine uses
        // the dispatcher created by runBlocking.
        scope1.launch {
            val scope2 = this
            // scope2 inherits from scope1
        }
    }
}
```
You might say that **CoroutineScope** formalizes the way the **CoroutineContext** is inherited. You can see how the **CoroutineScope** mediates the inheritance of coroutine contexts. If you cancel the job in `scope1`, this will propagate to `scope2` and will cancel the launched job as well.
