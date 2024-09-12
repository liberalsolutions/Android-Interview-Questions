### Q5: What is a purpose of Companion Objects in Kotlin? ☆☆☆

**Answer:**
Unlike Java or C#, Kotlin doesn’t have `static` members or member functions. If you need to write a function that can be called without having a class instance but needs access to the internals of a class, you can write it as a member of a **companion object** declaration inside that class.

```kotlin
class EventManager {

    companion object FirebaseManager {
    }  
}

val firebaseManager = EventManager.FirebaseManager
```

The companion object is a singleton. The companion object is a **proper object** on its own, and can have its own supertypes - and you can assign it to a variable and pass it around. If you're integrating with Java code and need a true static member, you can annotate a member inside a companion object with `@JvmStatic`.