### Q1. What is Android Room, and why is it used in Android app development?

Answer: Android Room is a part of the Android Jetpack library and is used as a SQLite object mapping library that makes it easier to work with databases in Android. It provides a higher-level abstraction over raw SQLite and offers compile-time verification of SQL queries. Room simplifies database operations and helps manage data persistence efficiently in Android apps.

### Q2. What are the core components of Android Room?

Answer: The core components of Android Room are:
* *Entity*: Represents a table in the database.
* *DAO (Data Access Object)*: Provides methods to interact with the database.
* *RoomDatabase*: Acts as the database holder and serves as the main entry point for accessing the database.

### Q3. How do you define an Entity in Android Room?

Answer: An Entity in Android Room is defined as a regular Kotlin data class with the `@Entity` annotation. Each property in the class represents a column in the database table, and you can use additional annotations like `@PrimaryKey` and `@ColumnInfo` to customize the entity's behavior and schema.

### Q4. What is a DAO in Android Room, and what is its role?

Answer: A DAO (Data Access Object) in Room is an interface that defines methods for performing database operations such as insertion, retrieval, updating, and deletion. It acts as a bridge between the Entity classes and the database, allowing you to execute SQL queries or methods to interact with the data.

### Q5. Explain the difference between LiveData and Flow in Room.

Answer: LiveData is a data holder class that is lifecycle-aware, meaning it automatically updates the UI when the data changes and respects the Android app’s lifecycle. Flow is a reactive stream provided by Kotlin, which can be used with Room to handle asynchronous data updates. While LiveData is designed specifically for Android, Flow is a more general-purpose reactive stream.

### Q6. How do you perform basic CRUD operations with Room?

To perform CRUD operations in Room:
* Use @Insert to insert data.
* Use @Query to read data.
* Use @Update to update data.
* Use @Delete to delete data.
* Define corresponding methods in the DAO interface.

### Q7. What is a Room Database Migration, and why might you need it?

A Room Database Migration is the process of modifying the database schema as the app evolves to handle changes such as adding new tables, columns, or modifying existing ones. Migrations ensure data integrity during database schema changes and prevent data loss.

### Q8. What is the role of the RoomDatabase class in Room?
Answer: The RoomDatabase class serves as the database holder and is responsible for managing database connections and providing access to DAOs. It is typically a singleton class in your application, and you can define database configurations within it.

### Q9. How can you ensure thread safety when working with Room?
You can ensure thread safety when working with Room by using appropriate concurrency mechanisms, such as running database operations on background threads using coroutines or LiveData


### Q10. What Are Room Auto-Migrations?

Auto-Migration is a feature allowing Room to automatically generate migration logic for certain schema changes. Auto-migrations simplify the process by automatically applying the necessary changes to the database schema when an app is updated.
It works best for:

* Adding new columns.
* Renaming columns.
* Dropping columns (with limitations).
* Adding or dropping tables.


### Q11. How Does Room Auto-Migration Work?
Room auto-migrations rely on annotations to detect changes in the database schema and automatically generate migration code. When you define your database version and schema, Room compares the schema differences between versions and creates the necessary SQL operations to apply changes during migration.

The key components are:

* @Database annotation: This is where the database version is incremented, and the auto-migration configuration is set up.
* AutoMigration annotation: Specifies the start and end versions between which Room should generate migration logic.


### Q12. How to Set Up Room Auto-Migration

Step 1: Defining the Initial Database Schema
```Kotlin
@Entity(tableName = "user")
data class User(
    @PrimaryKey(autoGenerate = true) val userId: Int,
    val name: String,
    val age: Int
)

@Database(entities = [User::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}
```
The database contains a single table user with three fields: userId, name, and age.
The database version is set to 1.

> How does Room handle relationships between entities?
> What are some best practices for optimizing database performance with Room?
> What is different between query and transaction in Room database?