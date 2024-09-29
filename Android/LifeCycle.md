### Q. What is the Android Activity lifecycle?

Explain the key lifecycle methods of an Activity (e.g., onCreate(), onStart(), onResume(), onPause(), onStop(), onDestroy()).

### Q. Can you explain the purpose of the onCreate() method in an Activity?

Oncreate() is used to set up the initial state of an Activity and load UI components using setContentView().

>### Q. What’s the difference between onStart() and onResume()?

* Visibility vs. Interactivity: onStart() makes the activity visible to the user, while onResume() makes the activity interactive and in the foreground.
* Order: onResume() is always called after onStart(), meaning the activity passes through the "started" state before it becomes fully resumed (interactive).
* Pausing vs. Stopping: When an activity is paused (partially obstructed, such as when a dialog is open), onResume() will be called again when it regains focus. However, when the activity is completely hidden (backgrounded), onStart() and onResume() will be called again when it returns to the foreground.

### Q. What is the difference between onPause() and onStop()?

Clarify the timing of onPause() vs. onStop() when the activity is no longer in the foreground but might still be visible (in the case of onPause()).

### Q. When should onSaveInstanceState() be used?

onSaveInstanceState() should be used to save UI-related transient data (like user input, selected items, etc.) before the activity is destroyed due to configuration changes or when it is sent to the background.
```Java
@Override
protected void onSaveInstanceState(Bundle outState) {
    super.onSaveInstanceState(outState);
    
    // Saving the user input from an EditText
    outState.putString("user_input", myEditText.getText().toString());
}

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // Restoring saved state
    if (savedInstanceState != null) {
        String savedInput = savedInstanceState.getString("user_input");
        myEditText.setText(savedInput);
    }
}
```

### Q. How do configuration changes like screen rotation affect the activity lifecycle?



### Q. What is the onRestoreInstanceState() method, and when is it called?
onRestoreInstanceState() is called after onStart() and is used to restore UI-related state that was saved in onSaveInstanceState().
```java
@Override
protected void onRestoreInstanceState(Bundle savedInstanceState) {
    super.onRestoreInstanceState(savedInstanceState);
    
    // Restoring state
    if (savedInstanceState != null) {
        String savedText = savedInstanceState.getString("user_input");
        myEditText.setText(savedText);
    }
}
```

### Q. How does the onBackPressed() method affect the activity lifecycle?
onBackPressed() can be overridden to customize the behavior when the user presses the back button. If not overridden, pressing the back button finishes the activity.
```Java
@Override
public void onBackPressed() {
    // Custom behavior, e.g., showing a confirmation dialog
    new AlertDialog.Builder(this)
        .setMessage("Are you sure you want to exit?")
        .setPositiveButton("Yes", (dialog, which) -> super.onBackPressed())
        .setNegativeButton("No", null)
        .show();
}
```

### Q. How does the activity lifecycle change when an Activity is launched in multi-window mode?

In multi-window mode, activities may remain partially visible. The activity lifecycle still calls onPause() when the activity is no longer focused, but onStop() is only called when the activity is completely hidden.

```Java
@Override
public void onMultiWindowModeChanged(boolean isInMultiWindowMode) {
    super.onMultiWindowModeChanged(isInMultiWindowMode);
    Log.d("Lifecycle", "Multi-window mode changed: " + isInMultiWindowMode);
}

@Override
protected void onPause() {
    super.onPause();
    Log.d("Lifecycle", "onPause called - Activity is partially visible");
}

@Override
protected void onStop() {
    super.onStop();
    Log.d("Lifecycle", "onStop called - Activity is fully hidden");
}
```

### Q. How does Android handle background tasks when an Activity is in onPause() or onStop()?
Background tasks should be managed using lifecycle-aware components like ViewModel and LiveData to avoid leaks.

// Example using LiveData to observe data only when the activity is in a resumed state
LiveData<String> liveData = new MutableLiveData<>();
liveData.observe(this, data -> {
    // Update UI only when the activity is in the foreground
    textView.setText(data);
});


### Q. What are the key methods in a Fragment lifecycle?


### Q. How is a Fragment's lifecycle different from an Activity's lifecycle?

onCreateView(): Inflates the fragment’s layout.
onViewCreated(): Called immediately after onCreateView(), used for additional view setup.

### Q. What is the difference between onCreateView() and onViewCreated() in a Fragment?


### Q. When is onDestroyView() used in a Fragment’s lifecycle?

### Q. How can you retain a Fragment’s state across configuration changes?


### Q. What is the use of FragmentTransaction and how does it affect the fragment lifecycle?


### Q. What are lifecycle-aware components in Android?


### Q. How do ViewModel and LiveData help manage the Android lifecycle effectively?**


### Q. What is the role of LifecycleObserver in Android?


### Q. Can you explain ProcessLifecycleOwner and its use case?


### Q. What happens if an activity is killed by the system? How can it be recovered?



### Q. How does the ActivityLifecycleCallbacks interface work?


### Q. Can you describe how services, especially IntentService and JobIntentService, interact with the lifecycle?

