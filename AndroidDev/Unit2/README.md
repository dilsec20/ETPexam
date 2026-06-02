# Unit 2: Managing Application Communication and Scheduling

---

## Key Definitions (Must Know for Viva)

| Keyword | Definition |
|---|---|
| **Intent** | A messaging object used to request an action from another app component. It is used to start activities, services, or deliver broadcasts. Intents can be **explicit** (target a specific component) or **implicit** (declare a general action). |
| **Explicit Intent** | An intent that specifies the exact component (class name) to start. Example: `Intent(this, SecondActivity::class.java)` — you know exactly which activity to launch. |
| **Implicit Intent** | An intent that declares a general action to perform, allowing the system to find a suitable component. Example: `Intent(Intent.ACTION_VIEW, Uri.parse("https://google.com"))` — the system decides which browser to open. |
| **Intent Filter** | A declaration in the AndroidManifest that specifies the types of intents a component can respond to. It defines `action`, `category`, and `data` elements. |
| **Pending Intent** | A wrapper around a regular Intent that grants permission to a foreign application (like AlarmManager or NotificationManager) to execute the contained Intent on your app's behalf, at a later time, even if your app is not running. |
| **PendingIntent Flag** | Flags that control the behavior of PendingIntent: `FLAG_UPDATE_CURRENT` (update existing), `FLAG_CANCEL_CURRENT` (cancel existing), `FLAG_IMMUTABLE` (cannot be modified), `FLAG_MUTABLE` (can be modified). |
| **FLAG_IMMUTABLE** | A PendingIntent flag indicating that the intent inside cannot be modified by the receiving app. Required for security on Android 12+ (API 31+). |
| **FLAG_MUTABLE** | A PendingIntent flag indicating the intent can be modified. Use when you need the system to fill in extras (e.g., inline reply in notifications). |
| **AlarmManager** | A system service that allows you to schedule your application to run at a specific time in the future. It can trigger PendingIntents at set times, even if the app is not running. |
| **Job Scheduler (JobScheduler)** | A system service that schedules background work based on conditions (network availability, charging state, idle). More battery-efficient than AlarmManager for background tasks. |
| **WorkManager** | A Jetpack library for deferrable, guaranteed background work. It is the recommended solution for persistent background tasks. It uses JobScheduler (API 23+) or AlarmManager + BroadcastReceiver internally. |
| **Notification** | A message displayed outside the app's UI to provide reminders, communication, or timely information. Shown in the notification bar/drawer. |
| **Notification Channel** | A category for notifications (required from Android 8.0 / API 26+). Each channel has its own importance level, sound, vibration, and light settings. Users can control each channel independently. |
| **NotificationManager** | A system service that manages notifications — creating, updating, and cancelling them. |
| **NotificationCompat.Builder** | A builder class to construct notifications with backward compatibility. |
| **BroadcastReceiver** | A component that listens for and responds to system-wide broadcast events (like alarm triggers, boot completed, battery low). |
| **Bundle** | A mapping from String keys to values, used to pass data between components via Intents (`intent.putExtra()` / `intent.getStringExtra()`). |
| **setExact()** | AlarmManager method that triggers an alarm at an exact time (for time-critical alarms). |
| **setRepeating()** | AlarmManager method that triggers an alarm repeatedly at a fixed interval. |
| **Context** | An interface that provides access to application-specific resources and classes, system services, and application-level operations. |

---

## 2.1 Intents

### Explicit Intent — Start Another Activity

```kotlin
// In MainActivity.kt
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            ExplicitIntentScreen(context = this)
        }
    }
}

@Composable
fun ExplicitIntentScreen(context: Context) {
    var name by remember { mutableStateOf("") }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        OutlinedTextField(
            value = name,
            onValueChange = { name = it },
            label = { Text("Enter your name") }
        )

        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = {
            // EXPLICIT INTENT - specifying the exact target class
            val intent = Intent(context, SecondActivity::class.java)
            intent.putExtra("USER_NAME", name)  // passing data
            context.startActivity(intent)
        }) {
            Text("Go to Second Activity")
        }
    }
}
```

```kotlin
// In SecondActivity.kt
class SecondActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // Receiving data from Intent
        val userName = intent.getStringExtra("USER_NAME") ?: "Unknown"

        setContent {
            Box(
                modifier = Modifier.fillMaxSize(),
                contentAlignment = Alignment.Center
            ) {
                Text("Welcome, $userName!", fontSize = 24.sp)
            }
        }
    }
}
```

> **Don't forget:** Register `SecondActivity` in `AndroidManifest.xml`:
```xml
<activity android:name=".SecondActivity" />
```

### Implicit Intent — Open a URL, Dial a Number, Share Text

```kotlin
@Composable
fun ImplicitIntentExamples(context: Context) {
    Column(
        modifier = Modifier.fillMaxSize().padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        // Open a website
        Button(onClick = {
            val intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com"))
            context.startActivity(intent)
        }) {
            Text("Open Website")
        }

        // Dial a phone number
        Button(onClick = {
            val intent = Intent(Intent.ACTION_DIAL, Uri.parse("tel:9876543210"))
            context.startActivity(intent)
        }) {
            Text("Dial Number")
        }

        // Send an email
        Button(onClick = {
            val intent = Intent(Intent.ACTION_SENDTO).apply {
                data = Uri.parse("mailto:test@example.com")
                putExtra(Intent.EXTRA_SUBJECT, "Hello")
                putExtra(Intent.EXTRA_TEXT, "This is a test email")
            }
            context.startActivity(intent)
        }) {
            Text("Send Email")
        }

        // Share text
        Button(onClick = {
            val intent = Intent(Intent.ACTION_SEND).apply {
                type = "text/plain"
                putExtra(Intent.EXTRA_TEXT, "Check out this app!")
            }
            context.startActivity(Intent.createChooser(intent, "Share via"))
        }) {
            Text("Share Text")
        }
    }
}
```

**Viva Q: What is the difference between Explicit and Implicit Intent?**
> **Explicit Intent** specifies the exact component to start (e.g., `SecondActivity::class.java`). Used for internal app navigation. **Implicit Intent** declares a general action (e.g., `ACTION_VIEW`), and the Android system finds a suitable app/component to handle it. Used for inter-app communication.

---

## 2.2 Pending Intents

### What is a PendingIntent?
A **PendingIntent** is a token that wraps a regular Intent and grants permission to an external app (like the system alarm service or notification manager) to execute that Intent on your app's behalf at a future time.

### Creating a PendingIntent

```kotlin
// PendingIntent to start an Activity
val intent = Intent(context, MainActivity::class.java)
val pendingIntent = PendingIntent.getActivity(
    context,
    0,                              // request code
    intent,
    PendingIntent.FLAG_IMMUTABLE    // required for Android 12+
)

// PendingIntent to start a BroadcastReceiver
val broadcastIntent = Intent(context, AlarmReceiver::class.java)
val pendingIntent = PendingIntent.getBroadcast(
    context,
    0,
    broadcastIntent,
    PendingIntent.FLAG_IMMUTABLE
)

// PendingIntent to start a Service
val serviceIntent = Intent(context, MyService::class.java)
val pendingIntent = PendingIntent.getService(
    context,
    0,
    serviceIntent,
    PendingIntent.FLAG_IMMUTABLE
)
```

---

## 2.3 Comparing Intents and Pending Intents

| Feature | Intent | PendingIntent |
|---|---|---|
| **Definition** | A messaging object to request an action | A wrapper around an Intent for deferred execution |
| **Execution** | Executed immediately by the app | Executed later by another app (system) |
| **Permissions** | Uses the calling app's permissions | Uses the creating app's permissions |
| **Use Case** | Start activities, services, broadcasts | Notifications, AlarmManager, widgets |
| **Who executes?** | Your app | Another app (NotificationManager, AlarmManager) |
| **Timing** | Now | In the future (deferred) |
| **Example** | `startActivity(intent)` | `AlarmManager.set(..., pendingIntent)` |

**Viva Q: Why do we need PendingIntent when we already have Intent?**
> A PendingIntent allows **another application** (like the system notification service) to perform an action **on behalf of your app** at a future time. The key is that it carries your app's identity and permissions, so even if your app is killed, the PendingIntent can still be executed by the system.

---

## 2.4 AlarmManager

### Setting an Alarm

```kotlin
// BroadcastReceiver to handle alarm
class AlarmReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        // Show a toast or notification when alarm triggers
        Toast.makeText(context, "Alarm Triggered!", Toast.LENGTH_LONG).show()
    }
}
```

```kotlin
// Setting alarm from Composable
@Composable
fun AlarmManagerExample(context: Context) {
    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Button(onClick = {
            val alarmManager = context.getSystemService(Context.ALARM_SERVICE)
                    as AlarmManager

            val intent = Intent(context, AlarmReceiver::class.java)
            val pendingIntent = PendingIntent.getBroadcast(
                context, 0, intent,
                PendingIntent.FLAG_IMMUTABLE
            )

            // Set alarm for 10 seconds from now
            val triggerTime = System.currentTimeMillis() + 10_000

            alarmManager.setExact(
                AlarmManager.RTC_WAKEUP,
                triggerTime,
                pendingIntent
            )

            Toast.makeText(context, "Alarm set for 10 seconds", Toast.LENGTH_SHORT).show()
        }) {
            Text("Set Alarm (10 sec)")
        }
    }
}
```

> **Register receiver in AndroidManifest.xml:**
```xml
<receiver android:name=".AlarmReceiver" android:exported="false" />
```

### AlarmManager Types:

| Type | Description |
|---|---|
| `RTC_WAKEUP` | Fires at specified time, wakes device from sleep |
| `RTC` | Fires at specified time, does NOT wake device |
| `ELAPSED_REALTIME_WAKEUP` | Fires after elapsed time since boot, wakes device |
| `ELAPSED_REALTIME` | Fires after elapsed time since boot, no wake |

**Viva Q: What is AlarmManager?**
> AlarmManager is a system service that schedules tasks to run at specific times in the future, even if the app is not running. It uses PendingIntents and can wake the device from sleep. It's suitable for time-critical tasks like alarms and reminders.

---

## 2.5 JobScheduler

```kotlin
// Define a JobService
class MyJobService : JobService() {
    override fun onStartJob(params: JobParameters?): Boolean {
        // Do background work here
        Log.d("MyJobService", "Job started!")

        // Return true if work is still ongoing (async)
        // Return false if work is done
        return false
    }

    override fun onStopJob(params: JobParameters?): Boolean {
        // Called if the job is cancelled before completion
        // Return true to reschedule, false to drop
        return true
    }
}
```

```kotlin
// Scheduling a Job
fun scheduleJob(context: Context) {
    val jobScheduler = context.getSystemService(Context.JOB_SCHEDULER_SERVICE)
            as JobScheduler

    val componentName = ComponentName(context, MyJobService::class.java)

    val jobInfo = JobInfo.Builder(1, componentName)
        .setRequiredNetworkType(JobInfo.NETWORK_TYPE_ANY)  // needs network
        .setRequiresCharging(true)                          // needs charging
        .setPeriodic(15 * 60 * 1000L)                      // every 15 min (minimum)
        .build()

    jobScheduler.schedule(jobInfo)
}
```

> **Register in AndroidManifest.xml:**
```xml
<service
    android:name=".MyJobService"
    android:permission="android.permission.BIND_JOB_SERVICE"
    android:exported="false" />
```

**Viva Q: What is the difference between AlarmManager and JobScheduler?**

| Feature | AlarmManager | JobScheduler |
|---|---|---|
| **Time-critical** | Yes (exact timing) | No (batched, deferred) |
| **Conditions** | None (time only) | Network, charging, idle |
| **Battery** | Higher battery usage | Battery-friendly |
| **API Level** | All versions | API 21+ |
| **Best for** | Alarms, reminders | Background sync, uploads |

---

## 2.6 Notifications

### Creating a Basic Notification

```kotlin
// Step 1: Create Notification Channel (required for API 26+)
fun createNotificationChannel(context: Context) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        val channel = NotificationChannel(
            "my_channel_id",                        // Channel ID
            "General Notifications",                // Channel Name
            NotificationManager.IMPORTANCE_HIGH     // Importance Level
        ).apply {
            description = "Channel for general notifications"
            enableLights(true)
            lightColor = Color.BLUE
            enableVibration(true)
        }

        val notificationManager = context.getSystemService(
            Context.NOTIFICATION_SERVICE
        ) as NotificationManager

        notificationManager.createNotificationChannel(channel)
    }
}
```

```kotlin
// Step 2: Build and Show Notification
fun showNotification(context: Context) {
    // Create intent to open when notification is tapped
    val intent = Intent(context, MainActivity::class.java)
    val pendingIntent = PendingIntent.getActivity(
        context, 0, intent,
        PendingIntent.FLAG_IMMUTABLE
    )

    val notification = NotificationCompat.Builder(context, "my_channel_id")
        .setSmallIcon(R.drawable.ic_notification)  // required
        .setContentTitle("Hello!")                  // required
        .setContentText("You have a new message")  // required
        .setPriority(NotificationCompat.PRIORITY_HIGH)
        .setContentIntent(pendingIntent)           // tap action
        .setAutoCancel(true)                       // dismiss on tap
        .build()

    val notificationManager = NotificationManagerCompat.from(context)
    notificationManager.notify(1, notification)    // 1 = notification ID
}
```

```kotlin
// Step 3: Use in Composable
@Composable
fun NotificationScreen(context: Context) {
    // Create channel when composable loads
    LaunchedEffect(Unit) {
        createNotificationChannel(context)
    }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Button(onClick = { showNotification(context) }) {
            Text("Show Notification")
        }
    }
}
```

### Notification Importance Levels:

| Importance | Behavior |
|---|---|
| `IMPORTANCE_HIGH` | Makes a sound and appears as heads-up notification |
| `IMPORTANCE_DEFAULT` | Makes a sound |
| `IMPORTANCE_LOW` | No sound |
| `IMPORTANCE_MIN` | No sound, no visual interruption |

---

## 2.7 Notification Channels

**Viva Q: What is a Notification Channel and why is it required?**
> From Android 8.0 (Oreo, API 26), all notifications MUST be assigned to a channel. Channels let users control notification behavior per category — they can mute, change sound, or disable specific channels without affecting others. Without a channel, notifications won't show on Android 8.0+.

### Multiple Channels Example:

```kotlin
fun createMultipleChannels(context: Context) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        val notificationManager = context.getSystemService(
            Context.NOTIFICATION_SERVICE
        ) as NotificationManager

        // Channel 1: Messages
        val messageChannel = NotificationChannel(
            "messages_channel",
            "Messages",
            NotificationManager.IMPORTANCE_HIGH
        ).apply {
            description = "New message notifications"
        }

        // Channel 2: Updates
        val updateChannel = NotificationChannel(
            "updates_channel",
            "App Updates",
            NotificationManager.IMPORTANCE_LOW
        ).apply {
            description = "App update notifications"
        }

        notificationManager.createNotificationChannel(messageChannel)
        notificationManager.createNotificationChannel(updateChannel)
    }
}
```

---

## Viva Questions & Answers

**Q1: What is an Intent?**
> An Intent is a messaging object used to request an action from another app component. It can start Activities, Services, or Broadcasts. It can carry data using `putExtra()`.

**Q2: What is a PendingIntent?**
> A PendingIntent is a wrapper around a regular Intent that allows another app (like the system) to execute the intent on your app's behalf at a future time, with your app's permissions, even if your app is killed.

**Q3: What is `FLAG_IMMUTABLE` in PendingIntent?**
> `FLAG_IMMUTABLE` means the PendingIntent cannot be modified by the app that receives it. It is required on Android 12+ for security. Use `FLAG_MUTABLE` only when the intent needs to be modified (e.g., inline reply in notifications).

**Q4: How do you pass data between activities?**
> Use `intent.putExtra("KEY", value)` to send data and `intent.getStringExtra("KEY")` (or `getIntExtra`, `getBooleanExtra`) to receive data in the target activity.

**Q5: What is a Notification Channel?**
> A notification channel is a category for grouping notifications (required from Android 8.0). Each channel has its own importance, sound, and vibration settings. Users can customize or mute individual channels.

**Q6: What are the three types of PendingIntent?**
> `PendingIntent.getActivity()` – to start an Activity, `PendingIntent.getBroadcast()` – to trigger a BroadcastReceiver, `PendingIntent.getService()` – to start a Service.

**Q7: What is WorkManager and when should you use it?**
> WorkManager is a Jetpack library for **deferrable, guaranteed** background work. Use it when work must eventually complete even if the app is killed or device restarts (e.g., syncing data, uploading files). It is the recommended solution over AlarmManager and JobScheduler for most background tasks.

**Q8: What is a BroadcastReceiver?**
> A BroadcastReceiver is a component that listens for system-wide broadcast messages (intents). It responds to events like alarm triggers, boot completion, or network changes. It has an `onReceive()` method.

**Q9: Can you show a notification without creating a channel?**
> On Android 7.1 (API 25) and below, yes — channels are not needed. On Android 8.0 (API 26) and above, NO — you must create a NotificationChannel first, or the notification won't display.

**Q10: What is `Intent.ACTION_VIEW` vs `Intent.ACTION_SEND`?**
> `ACTION_VIEW` is used to display data to the user (open a URL, view a map, play a video). `ACTION_SEND` is used to share data with another app (share text, image via WhatsApp, email).

---
