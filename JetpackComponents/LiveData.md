### 1. What is LiveData in Android?
LiveData is an observable data holder class in Android architecture components that is lifecycle-aware. It ensures that the UI components (like Activity, Fragment, or ViewModel) only observe changes in the data when they are in an active lifecycle state (e.g., STARTED or RESUMED). This helps avoid memory leaks and prevents the UI from updating when it's not visible.

### 2. What are the advantages of using LiveData?
Answer:

* Lifecycle-aware: Automatically stops updating the UI if the observing lifecycle (e.g., Activity or Fragment) is not in an active state.
* No memory leaks: Observers are automatically removed when their lifecycle owner (like an Activity) is destroyed.
* Data synchronization: Ensures UI stays updated with the latest data.
*vHandles configuration changes: LiveData survives configuration changes like screen rotations without needing to reload data.
* Decouples UI logic from data: ViewModel holds LiveData, keeping UI logic separate from the data layer.

### 3. How does LiveData differ from an Observable?
Answer:

Lifecycle-awareness: LiveData is lifecycle-aware, meaning it only updates active observers (e.g., when the Activity or Fragment is in the STARTED or RESUMED state), while traditional observables are not and can update regardless of the observer's state.
No manual management: With LiveData, you don’t have to manually handle lifecycle events to stop or resume updates. Observables require developers to manage this.
Memory management: LiveData automatically handles memory leaks by removing inactive observers, while you need to manually clean up observers in traditional observables.

### 4. What is `MutableLiveData`, and how does it differ from `LiveData`?
Answer:

`LiveData`: Is read-only, meaning that it only allows observing data but does not allow modifications to the data.
`MutableLiveData`: Extends LiveData and allows both observing and updating the data. It provides methods like setValue() or postValue() to update the underlying data.

### 5. What is the difference between setValue() and postValue() in MutableLiveData?
Answer:

setValue(): Updates the value of LiveData on the main thread. This should be used when you're modifying LiveData from the main (UI) thread.
postValue(): Posts an update to LiveData asynchronously on a background thread. The change will be made when the main thread processes it..
```Java
// Example:
mutableLiveData.setValue("New Value")  // Call on the main thread
mutableLiveData.postValue("New Value") // Call from a background thread
```

### 6. How does LiveData handle configuration changes such as screen rotations?
Answer:
`LiveData` works seamlessly with `ViewModel` to handle configuration changes like screen rotations. Since `ViewModel` is retained during configuration changes, it continues to hold the LiveData, and the observers (UI components) are re-attached after the configuration change. The data does not need to be re-fetched or recomputed, preventing redundant operations.

### 7. What is MediatorLiveData, and when would you use it?
Answer:
MediatorLiveData is a subclass of LiveData that can observe multiple LiveData sources and react to their changes. You can use it when you want to combine data from multiple LiveData sources into one LiveData.
```Java
// Example:
val liveData1 = MutableLiveData<String>()
val liveData2 = MutableLiveData<String>()

val mediatorLiveData = MediatorLiveData<String>()

mediatorLiveData.addSource(liveData1) { value ->
    mediatorLiveData.value = "LiveData1: $value"
}

mediatorLiveData.addSource(liveData2) { value ->
    mediatorLiveData.value = "LiveData2: $value"
}
```
### 8. How can you observe LiveData in a Fragment or Activity?

Answer:
You can observe LiveData using the observe() method, which takes a LifecycleOwner (e.g., Activity, Fragment) and an observer (Observer<T>) that reacts to changes.
```java
viewModel.liveData.observe(viewLifecycleOwner) { data ->
    // Update UI with the observed data
}
```
The observe() method ensures that the observer only gets updates when the Fragment or Activity is in an active state (i.e., started or resumed).


### 9. How does LiveData ensure thread safety?
Answer:
LiveData is thread-safe because it ensures that the setValue() method (used to update the LiveData) can only be called on the main thread. If updates need to happen from a background thread, you must use postValue(), which internally schedules the update to happen on the main thread.

### 10. LiveData vs Flow in Android

> I have to read the LiveData vs Flow again