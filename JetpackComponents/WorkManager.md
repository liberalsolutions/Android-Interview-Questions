### Q1. What is Android WorkManager?

Answer: Android WorkManager is an API introduced by Google to simplify and manage background tasks in Android applications. It serves as a unified solution that abstracts away the differences between various versions of Android and their limitations regarding background processing. WorkManager enables developers to schedule and execute tasks reliably, even across device reboots.

### Q2. What are the key features of WorkManager?
WorkManager offers several essential features, including:

* Support for one-time and periodic tasks.
* Ability to define constraints for task execution, such as network availability or device charging status.
* Guaranteed task execution, even across device reboots.
* Seamless integration with other Jetpack components, such as LiveData and ViewModel.


### Q3. How can you pass data to a Worker class?

You can pass data to a Worker class by using the `setInputData()` method when creating the WorkRequest. This method allows you to attach a Data object containing `key-value` pairs. Inside the Worker's `doWork()` method, you can retrieve the data using the `getInputData()` method.

```Java
Data inputData = new Data.Builder()
    .putString("key", "value")
    .build();

OneTimeWorkRequest myWorkRequest = new OneTimeWorkRequest.Builder(MyWorker.class)
    .setInputData(inputData)
    .build();
```

### Q4. How can you observe the progress or output of a Worker class?

WorkManager provides a LiveData object called `WorkInfo` that allows you to observe the progress and status of a Worker. By using the `getWorkInfoByIdLiveData()` method, you can obtain the `WorkInfo` object and observe it to get updates on the task's progress, output, and completion status.

```Java
WorkManager.getInstance(context).getWorkInfoByIdLiveData(workRequestId)
    .observe(owner, workInfo -> {
        if (workInfo != null && workInfo.getState().isFinished()) {
            // Task finished
            // Access output data: workInfo.getOutputData()
        } else {
            // Task in progress
            // Access progress: workInfo.getProgress()
        }
    });

```
### Q5. How can you chain multiple work requests together?
To chain multiple work requests together, you can use the `then()` method on a WorkRequest object. This method allows you to specify another WorkRequest that should run after the current one completes. By chaining work requests, you can define a sequence of tasks and ensure they are executed in the desired order.

```Java
OneTimeWorkRequest firstWorkRequest = new OneTimeWorkRequest.Builder(FirstWorker.class).build();
OneTimeWorkRequest secondWorkRequest = new OneTimeWorkRequest.Builder(SecondWorker.class).build();

WorkManager.getInstance(context)
    .beginWith(firstWorkRequest)
    .then(secondWorkRequest)
    .enqueue();
```

### Q6. How can you handle and retry failed tasks in WorkManager?
WorkManager automatically handles failed tasks by respecting the retry policy defined for the WorkRequest. You can specify the retry policy using the `setBackoffCriteria()` method, which allows you to define the initial and maximum delay for retries. WorkManager intelligently applies exponential backoff to retries, giving failed tasks a chance to succeed without overwhelming system resources.

```Java
// Set exponential backoff with a 1-minute initial delay and a maximum of 3 retries
OneTimeWorkRequest myWorkRequest = new OneTimeWorkRequest.Builder(MyWorker.class)
    .setBackoffCriteria(BackoffPolicy.EXPONENTIAL, OneTimeWorkRequest.MIN_BACKOFF_MILLIS, TimeUnit.MILLISECONDS)
    .build();
```

### Q7. What is the difference between WorkManager, JobScheduler, and AlarmManager?

* `WorkManager` is a modern, flexible API that handles background work efficiently with guaranteed execution.
* `JobScheduler` is used to schedule jobs that run in the background, but it doesn't work below Android Lollipop.
* `AlarmManager` schedules alarms, but it doesn’t guarantee task completion.
* `WorkManager` is a unified API that works across all API levels, handling the limitations of `JobScheduler` and `AlarmManager`

### Q8. What are the types of WorkRequests in WorkManager?
* OneTimeWorkRequest: Used to execute a task once.
* PeriodicWorkRequest: Used to execute a task repeatedly at specified intervals.

### Q9. What are the Worker, WorkRequest, and WorkManager components?

* `Worker`: The unit of work that performs the task in a background thread.
* `WorkRequest`: Defines how and when the work should be executed (e.g., `OneTimeWorkRequest`, `PeriodicWorkRequest`).
* `WorkManager`: The system service responsible for managing and scheduling WorkRequests.

### Q10. What are Constraints in WorkManager?

Constraints specify the conditions under which the work will run, like network availability, device charging state, battery level, etc. Example of setting constraints:
```Java
val constraints = Constraints.Builder()
    .setRequiredNetworkType(NetworkType.CONNECTED)
    .setRequiresCharging(true)
    .build()
```

### Q11. How do you cancel a WorkRequest in WorkManager?
You can cancel a work request using its ID or a tag:
```Kotlin
WorkManager.getInstance(context).cancelWorkById(workRequestId)
```

### Q12. WorkManager.getInstance(context).cancelWorkById(workRequestId)
* `Result.success()`: Indicates the task was completed successfully.
* `Result.retry()`: Indicates the task failed but should be retried later.
* `Result.failure()`: Indicates the task failed permanently, and no retry is needed.

### Q13. What is PeriodicWorkRequest and how does it work?
PeriodicWorkRequest schedules repetitive tasks with a minimum interval of 15 minutes. It's used when you need to execute a task periodically
```Java
val periodicWorkRequest = PeriodicWorkRequestBuilder<MyWorker>(15, TimeUnit.MINUTES).build()
WorkManager.getInstance(context).enqueue(periodicWorkRequest)
```

### Q14. What is the maximum time delay for PeriodicWorkRequest in WorkManager?
The `minimum` delay for `PeriodicWorkRequest` is 15 minutes. There is no maximum delay, but you can specify any value beyond 15 minutes.

### Q15. How does WorkManager handle task completion when the device restarts?
` ` is persistent, and tasks will be rescheduled after a device reboot as long as the work is not completed. For work to survive a reboot, you need to include the `RECEIVE_BOOT_COMPLETED` permission in your manifest.