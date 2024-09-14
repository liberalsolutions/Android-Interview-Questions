### Q1. What is the difference between a Service and an IntentService in Android?

**Answer**: Both Service and IntentService are used to perform background operations in Android. The main difference lies in how they handle requests. A Service runs on the main thread and requires manual handling of background tasks and thread management. On the other hand, IntentService automatically creates a worker thread for each start request and handles requests sequentially, making it more suitable for simple, independent background tasks.

### Q2. Explain the concept of Broadcast Receivers in Android.

**Answer**: Broadcast Receivers are components in Android that enable communication between the system and the application or between different applications. They allow an application to receive and respond to system-wide events or custom-defined events. For example, a BroadcastReceiver can listen for events such as device boot, network connectivity changes, incoming SMS, or custom broadcast messages. It helps in implementing event-driven behavior in Android applications.