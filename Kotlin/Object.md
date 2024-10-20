### Q16: How to create singleton in Kotlin? ☆☆

**Answer:**
Just use `object`.
```kotlin
object SomeSingleton
```
The above Kotlin object will be compiled to the following equivalent Java code:
```java
public final class SomeSingleton {
   public static final SomeSingleton INSTANCE;

   private SomeSingleton() {
      INSTANCE = (SomeSingleton)this;
      System.out.println("init complete");
   }

   static {
      new SomeSingleton();
   }
}
```
This is the preferred way to implement singletons on a JVM because it enables thread-safe lazy initialization without having to rely on a locking algorithm like the complex double-checked locking.

### Q16: How would you create a singleton with parameter in Kotlin? ☆☆☆

**Answer:**
Because a Kotlin `object` can’t have any constructor, you can’t pass any argument to it.

So look at this code from Google's architecture components sample code, which uses the `also` function:

```kotlin
class UsersDatabase : RoomDatabase() {

    companion object {

        @Volatile private var INSTANCE: UsersDatabase? = null

        fun getInstance(context: Context): UsersDatabase =
            INSTANCE ?: synchronized(this) {
                INSTANCE ?: buildDatabase(context).also { INSTANCE = it }
            }

        private fun buildDatabase(context: Context) =
            Room.databaseBuilder(context.applicationContext,
                    UsersDatabase::class.java, "Sample.db")
                    .build()
    }
}
```