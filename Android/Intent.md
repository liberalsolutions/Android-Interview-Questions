### Q1. What is an Intent in Android?
An Intent is an object used to request an action from another app component. It is used for communication between components, such as starting activities, services, or sending broadcasts.

Intent intent = new Intent(MainActivity.this, SecondActivity.class);
startActivity(intent);

### Q2. What are the types of Intents in Android?
Explicit Intent: Specifies the exact component (activity/service) to start. Used for communication within the same application.
Implicit Intent: Specifies an action to be performed without specifying the component. The system determines the appropriate component (like launching a web browser, email client, etc.).

// Explicit Intent
Intent intent = new Intent(MainActivity.this, SecondActivity.class);
startActivity(intent);

// Implicit Intent
Intent intent = new Intent(Intent.ACTION_VIEW);
intent.setData(Uri.parse("https://www.example.com"));
startActivity(intent);

### Q3. What are Intent Filters in Android?
An Intent Filter is used to declare the capabilities of a component. It allows the system to match implicit intents to the appropriate components. For example, if an app wants to handle URLs, it can declare an intent filter for ACTION_VIEW and http URLs.
```xml
<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <data android:scheme="http" />
</intent-filter>
```

### Q4. What is the role of Intent in startService() and bindService()?
* startService(): An Intent is used to start a service for performing background tasks.
* bindService(): An Intent is used to bind a service to an activity, allowing interaction with it.
```Java
// Starting a service
Intent serviceIntent = new Intent(this, MyService.class);
startService(serviceIntent);

// Binding to a service
Intent bindIntent = new Intent(this, MyService.class);
bindService(bindIntent, serviceConnection, Context.BIND_AUTO_CREATE);
```

### Q5. What is a PendingIntent in Android?
A PendingIntent is a token that you give to a foreign application (e.g., NotificationManager, AlarmManager), which allows the application to execute an action on your app's behalf, later.

Intent intent = new Intent(this, MainActivity.class);
PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);
```Java
// Example: Using PendingIntent in a Notification
Notification notification = new Notification.Builder(this)
        .setContentTitle("Title")
        .setContentText("Message")
        .setSmallIcon(R.drawable.icon)
        .setContentIntent(pendingIntent)
        .build();
```

### Q6. How do you handle incoming intents in an activity?
To handle incoming intents, check the intent data in onCreate() or onNewIntent() if the activity is launched in singleTop mode.
```Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    Intent intent = getIntent();
    if (Intent.ACTION_VIEW.equals(intent.getAction())) {
        Uri uri = intent.getData();
        // Handle the URI
    }
}
```