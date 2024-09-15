### Q. What is a Sealed Class?

A sealed class is a class that is marked with the `sealed` keyword in Kotlin. It is used to define a *closed set of subclasses*. It allows you to define a *restricted class hierarchy* in which subclasses are *predefined* and *finite*. The subclasses of a sealed class are defined within the sealed class itself, and each `subclass` must be declared as `inner` or `data` or `class`, with *no other modifiers allowed*.

### Q. Syntax of a Sealed Class:
```Kotlin
sealed class SealedClassName {
    // Subclasses
    class SubclassName1 : SealedClassName()
    class SubclassName2 : SealedClassName()
    // ...
}
```

### Q. Use Cases of Sealed Classes:

Sealed classes are useful in many situations where you have a fixed set of possible classes that need to be represented. Here are some common use cases for sealed classes:

* *Representing the Result of an Operation:*
One common use case for sealed classes is to represent the result of an operation. For example, We might define a sealed class called `Result` with two subclasses: `Success` and `Error`.
```Kotlin
sealed class Result {
    data class Success(val data: String) : Result()
    data class Error(val message: String) : Result()
}
```

With this definition, We can use a `when` expression to handle all possible cases of `Result`, like this:

```kotlin
fun handleResult(result: Result) {
    when(result) {
        is Result.Success -> println(result.data)
        is Result.Error -> println(result.message)
    }
}
```
* *State Machine:*

Another common use case for sealed classes is to represent the states of a *state machine*. For example, We might define a sealed class called State with subclasses representing different `states` of a game.

```kotlin
sealed class State {
    object Initial : State()
    object Running : State()
    object Paused : State()
    object Finished : State()
}
```

With this definition, we can use a when expression to handle all possible cases of `State`, like this:
```kotlin
fun handleState(state: State) {
    when(state) {
        is State.Initial -> println("The game is starting...")
        is State.Running -> println("The game is running...")
        is State.Paused -> println("The game is paused...")
        is State.Finished -> println("The game is finished!")
    }
}
```

* *Handling UI States:*

A common use case for sealed classes is handling different UI states in Android applications. For example, you might define a sealed class called `ViewState` subclasses representing different UI states of a screen.
```kotlin
sealed class ViewState {
    object Loading : ViewState()
    data class Success(val data: List<String>) : ViewState()
    data class Error(val message: String) : ViewState()
}
```

With this definition, We can use an `when` expression to handle all possible cases of `ViewState`, like this:
```kotlin
fun handleViewState(viewState: ViewState) {
    when(viewState) {
      is ViewState.Loading -> showLoadingIndicator()
      is ViewState.Success -> showData(viewState.data)
      is ViewState.Error -> showError(viewState.message)
  }
}
```

### Advantages Over Enum Classes

Sealed classes can hold different types of data and can have state, unlike enums which are limited to a predefined set of constants without state.



















### Here are some more examples of how sealed classes can be used to implement design patterns:

https://medium.com/@summitkumar/unlocking-the-power-of-sealed-classes-in-kotlin-design-patterns-and-better-code-organization-5627d73a4903