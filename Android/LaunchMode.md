### Q. What is Launch Mode in Android?

Launch mode is an Android OS command that determines how the activity should be started.

### Q2. Types of Launch Mode in Android?

1. Standard
2. SingleTop
3. SingleTask
4. SingleInstance
### Q3. What is Standard Mode?
* This mode launches a new instance of an activity in the task. This mode can create multiple instances of the same activity, and these can be assigned to the same or separate tasks.
* This is the default launch mode of activity. If you don’t set any launch mode to your activity, it will use the standard mode by default. It creates a new instance of activity every time even if activity instance is already present.

### Q4. What is SingleTop Mode?
* If an instance of activity already exists at the top of the current task, a new instance will not be created and the Android system will route the intent information through onNewIntent().
* If an instance is not present on top of the task then a new instance will be created.

### Q6. What is SingleTask Mode?
* An activity declared with launch mode as singleTask can have only one instance in the system (singleton). At a time only one instance of activity will exist.

### Q7. What is SingleInstance Mode?

* This mode is similar to singleTask mode, but the major difference is that the activity is launched in a new task and this task cannot have any other activities.
* If another Activity is called from this kind of Activity, a new Task would be automatically created to place that new Activity.

### Q8. Suppose we have A, B, C, and D activities and your activity B has `standard` launch mode. Now again launching activity B. What will be the State of Activity Stack before and after launch B?

State of Activity Stack before launch B

A →B→ C→D

State of Activity Stack after launch B

A → B → C→D→ B

We can see that new instance of B is created again.

### Q9. Let’s say you have 4 different activities, A, B, C and D and they were launched in order and and your activity D has `SingleTop` launch mode If you launch activity D again What will be the State of Activity Stack before and after launch D?

State of Activity Stack before launch D
> A -> B -> C -> D
State of Activity Stack after launch D
> A -> B -> C -> D where activity D is not created again

### Q10. Let’s say you have 4 different activities, A, B, C and D and they were launched in order and and your activity D has `standard` launch mode If you launch activity D again What will be the State of Activity Stack before and after launch D?
State of Activity Stack before launch D
> A -> B -> C -> D
State of Activity Stack after launch D
> A -> B -> C -> D -> D

### Q11. Let’s say you have 4 different activities, A, B, C and D and they were launched in order and and your activity B has `SingleTop` launch mode If you launch activity B again What will be the State of Activity Stack before and after launch B?

State of Activity Stack before launch B
> A -> B -> C -> D
State of Activity Stack after launch B
> A -> B -> C -> D -> B where activity B is created again because even though it was in the backstack, it was not at the top

### Q12. Let’s say you have 4 different activities, A, B, C and D and they were launched in order and and your activity D has `singleTask` launch mode If you launch activity D again What will be the State of Activity Stack before and after launch D?

State of Activity Stack before launch D
> A -> B -> C -> D
State of Activity Stack after launch D
> A -> B -> C -> D where activity D is not created again


### Q13. Let’s say you have 4 different activities, A, B, C and D and A,B, C were launched in order and and your activity D has `singleTask` launch mode If you launch activity D again What will be the State of Activity Stack before and after launch D?

State of Activity Stack before launch D
> A -> B -> C 
State of Activity Stack after launch D
> A -> B -> C -> D where activity D is created

### Q14. Let’s say you have 4 different activities, A, B, C and D and they were launched in order and and your activity B has `singleTask` launch mode If you launch activity B again What will be the State of Activity Stack before and after launch B?

State of Activity Stack before launch B
> A -> B -> C -> D
State of Activity Stack after launch B
> A -> B where activity B is brought to the top of the stack in its old state and other activities on top of the activity B is destroyed

### Q 15. Let’s say you have 4 different activities, A, B, C and D and A, B, C were launched in order and and your activity D has `singleInstance` launch mode If you launch activity D again What will be the State of Activity Stack before and after launch D?

State of Activity Stack before launch D
> A -> B -> C 
State of Activity Stack after launch D
> A -> B -> C  where the activity D is created in a separate task (Task2)

### Q16. Let’s say you have 5 different activities, A, B, C, D and E and A, B, C were launched in order and and your activity D has `singleInstance` launch mode If you launch activity D  What will be the State of Activity Stack before and after launch D? And What will happen if We launch Activity E, which we’ll assume isn’t on singleInstance mode?

>Task1: A -> B -> C -> E

>Task2: D where activity E is created on task1.

### Q17. Let’s say you have 5 different activities, A, B, C, D and E and A, B, C were launched in order and and your activity D has `singleInstance` launch mode If you launch activity D  What will be the State of Activity Stack before and after launch D? And What will happen if We launch Activity E, which is on singleInstance mode?

### Q

### Q
