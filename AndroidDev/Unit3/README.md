# Unit 3: Notifications and User Interaction

---

## Key Definitions (Must Know for Viva)

| Keyword | Definition |
|---|---|
| **Notification** | A message displayed outside the app's normal UI, in the system notification bar, providing information, reminders, or communication from an app to the user. |
| **Notification Channel** | A category/group for notifications (required from Android 8.0 / API 26+). Each channel can have its own importance, sound, vibration, and light settings. Users can independently control each channel. |
| **NotificationManager** | A system service responsible for posting, updating, and cancelling notifications. |
| **NotificationCompat.Builder** | A backward-compatible builder class used to construct notification objects with title, text, icon, actions, and other properties. |
| **IMPORTANCE_HIGH** | Channel importance level that makes sound and shows a heads-up (floating) notification. |
| **IMPORTANCE_DEFAULT** | Channel importance level that makes sound but no heads-up notification. |
| **IMPORTANCE_LOW** | Channel importance level with no sound. |
| **IMPORTANCE_MIN** | Channel importance level with no sound and no visual interruption. |
| **setAutoCancel** | When set to `true`, the notification is automatically dismissed when the user taps on it. |
| **setContentIntent** | Sets the PendingIntent that will be fired when the user taps the notification body. |
| **addAction** | Adds an action button to a notification (e.g., Reply, Dismiss). |
| **BigTextStyle** | An expandable notification style that shows a large block of text when expanded. |
| **InboxStyle** | An expandable notification style that shows a list of strings (like email summaries). |
| **BigPictureStyle** | An expandable notification style that shows a large image. |
| **DatePickerDialog** | A dialog that allows the user to select a date (day, month, year) from a calendar interface. |
| **TimePickerDialog** | A dialog that allows the user to select a time (hour, minute) using a clock interface. |
| **DatePicker** | A Compose Material3 composable for picking dates within a dialog. |
| **TimePicker** | A Compose Material3 composable for picking time within a dialog. |
| **Dialog** | A small window that prompts the user for a decision or additional information. In Compose, created using the `Dialog` or `AlertDialog` composable. |
| **AlertDialog** | A dialog with a title, message, and action buttons (confirm/dismiss). |
| **rememberDatePickerState** | A state holder for the DatePicker composable that remembers the selected date. |
| **rememberTimePickerState** | A state holder for the TimePicker composable that remembers the selected time. |
| **POST_NOTIFICATIONS** | A runtime permission required from Android 13 (API 33+) to show notifications. |

---

## 3.1 Notifications (Detailed)

### Complete Notification Example with Channel

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        createNotificationChannel()
        setContent {
            NotificationDemoScreen(this)
        }
    }

    private fun createNotificationChannel() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            val channel = NotificationChannel(
                "main_channel",
                "Main Notifications",
                NotificationManager.IMPORTANCE_HIGH
            ).apply {
                description = "Primary notification channel"
                enableLights(true)
                lightColor = android.graphics.Color.RED
                enableVibration(true)
                vibrationPattern = longArrayOf(0, 250, 250, 250)
            }

            val manager = getSystemService(NotificationManager::class.java)
            manager.createNotificationChannel(channel)
        }
    }
}
```

### Simple Notification

```kotlin
@Composable
fun NotificationDemoScreen(context: Context) {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(24.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.spacedBy(16.dp, Alignment.CenterVertically)
    ) {
        // Simple Notification
        Button(onClick = {
            showSimpleNotification(context)
        }) {
            Text("Simple Notification")
        }

        // Big Text Notification
        Button(onClick = {
            showBigTextNotification(context)
        }) {
            Text("Big Text Notification")
        }

        // Notification with Actions
        Button(onClick = {
            showActionNotification(context)
        }) {
            Text("Notification with Actions")
        }
    }
}
```

```kotlin
fun showSimpleNotification(context: Context) {
    val intent = Intent(context, MainActivity::class.java)
    val pendingIntent = PendingIntent.getActivity(
        context, 0, intent, PendingIntent.FLAG_IMMUTABLE
    )

    val notification = NotificationCompat.Builder(context, "main_channel")
        .setSmallIcon(R.drawable.ic_launcher_foreground)
        .setContentTitle("New Message")
        .setContentText("You have received a new message")
        .setPriority(NotificationCompat.PRIORITY_HIGH)
        .setContentIntent(pendingIntent)
        .setAutoCancel(true)
        .build()

    NotificationManagerCompat.from(context).notify(101, notification)
}
```

### Big Text Style Notification

```kotlin
fun showBigTextNotification(context: Context) {
    val notification = NotificationCompat.Builder(context, "main_channel")
        .setSmallIcon(R.drawable.ic_launcher_foreground)
        .setContentTitle("Long Message")
        .setContentText("This is a summary of the message...")
        .setStyle(
            NotificationCompat.BigTextStyle()
                .bigText("This is a very long notification message that " +
                         "will be fully visible when the user expands the " +
                         "notification. It can contain multiple lines of text " +
                         "to provide detailed information to the user.")
                .setBigContentTitle("Expanded Title")
                .setSummaryText("Summary")
        )
        .setPriority(NotificationCompat.PRIORITY_HIGH)
        .setAutoCancel(true)
        .build()

    NotificationManagerCompat.from(context).notify(102, notification)
}
```

### Notification with Action Buttons

```kotlin
fun showActionNotification(context: Context) {
    // Action: Open app
    val openIntent = Intent(context, MainActivity::class.java)
    val openPending = PendingIntent.getActivity(
        context, 0, openIntent, PendingIntent.FLAG_IMMUTABLE
    )

    // Action: Dismiss (broadcast)
    val dismissIntent = Intent(context, DismissReceiver::class.java)
    val dismissPending = PendingIntent.getBroadcast(
        context, 0, dismissIntent, PendingIntent.FLAG_IMMUTABLE
    )

    val notification = NotificationCompat.Builder(context, "main_channel")
        .setSmallIcon(R.drawable.ic_launcher_foreground)
        .setContentTitle("Download Complete")
        .setContentText("File has been downloaded successfully")
        .setPriority(NotificationCompat.PRIORITY_HIGH)
        .addAction(R.drawable.ic_open, "Open", openPending)
        .addAction(R.drawable.ic_dismiss, "Dismiss", dismissPending)
        .setAutoCancel(true)
        .build()

    NotificationManagerCompat.from(context).notify(103, notification)
}
```

---

## 3.2 Implementing Notification Channels

### Multiple Channels

```kotlin
fun createAllChannels(context: Context) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
        val manager = context.getSystemService(NotificationManager::class.java)

        // Channel 1: Chat messages (High priority)
        val chatChannel = NotificationChannel(
            "chat_channel",
            "Chat Messages",
            NotificationManager.IMPORTANCE_HIGH
        ).apply {
            description = "Notifications for new chat messages"
            enableLights(true)
            enableVibration(true)
        }

        // Channel 2: Promotions (Low priority)
        val promoChannel = NotificationChannel(
            "promo_channel",
            "Promotions",
            NotificationManager.IMPORTANCE_LOW
        ).apply {
            description = "Promotional offers and updates"
        }

        // Channel 3: System alerts (Default priority)
        val systemChannel = NotificationChannel(
            "system_channel",
            "System Alerts",
            NotificationManager.IMPORTANCE_DEFAULT
        ).apply {
            description = "System-level alerts and updates"
        }

        manager.createNotificationChannel(chatChannel)
        manager.createNotificationChannel(promoChannel)
        manager.createNotificationChannel(systemChannel)
    }
}
```

```kotlin
// Send notification to specific channel
fun sendChatNotification(context: Context, message: String) {
    val notification = NotificationCompat.Builder(context, "chat_channel")  // specific channel
        .setSmallIcon(R.drawable.ic_chat)
        .setContentTitle("New Chat")
        .setContentText(message)
        .setPriority(NotificationCompat.PRIORITY_HIGH)
        .setAutoCancel(true)
        .build()

    NotificationManagerCompat.from(context).notify(201, notification)
}

fun sendPromoNotification(context: Context) {
    val notification = NotificationCompat.Builder(context, "promo_channel")  // different channel
        .setSmallIcon(R.drawable.ic_promo)
        .setContentTitle("Special Offer!")
        .setContentText("50% off on all items today!")
        .setPriority(NotificationCompat.PRIORITY_LOW)
        .setAutoCancel(true)
        .build()

    NotificationManagerCompat.from(context).notify(202, notification)
}
```

---

## 3.3 Date Picker Dialog

### Using Material3 DatePicker in Compose

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun DatePickerExample() {
    var showDatePicker by remember { mutableStateOf(false) }
    var selectedDate by remember { mutableStateOf("No date selected") }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text(text = selectedDate, fontSize = 20.sp)

        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = { showDatePicker = true }) {
            Text("Pick a Date")
        }
    }

    if (showDatePicker) {
        val datePickerState = rememberDatePickerState()

        DatePickerDialog(
            onDismissRequest = { showDatePicker = false },
            confirmButton = {
                TextButton(onClick = {
                    // Convert millis to date string
                    datePickerState.selectedDateMillis?.let { millis ->
                        val sdf = SimpleDateFormat("dd/MM/yyyy", Locale.getDefault())
                        selectedDate = sdf.format(Date(millis))
                    }
                    showDatePicker = false
                }) {
                    Text("OK")
                }
            },
            dismissButton = {
                TextButton(onClick = { showDatePicker = false }) {
                    Text("Cancel")
                }
            }
        ) {
            DatePicker(state = datePickerState)
        }
    }
}
```

### Using Android's Built-in DatePickerDialog (Alternative)

```kotlin
@Composable
fun AndroidDatePickerExample(context: Context) {
    var selectedDate by remember { mutableStateOf("No date selected") }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text(text = selectedDate, fontSize = 20.sp)
        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = {
            val calendar = Calendar.getInstance()
            val year = calendar.get(Calendar.YEAR)
            val month = calendar.get(Calendar.MONTH)
            val day = calendar.get(Calendar.DAY_OF_MONTH)

            DatePickerDialog(
                context,
                { _, selectedYear, selectedMonth, selectedDay ->
                    selectedDate = "$selectedDay/${selectedMonth + 1}/$selectedYear"
                },
                year, month, day
            ).show()
        }) {
            Text("Pick Date")
        }
    }
}
```

**Viva Q: How do you implement a Date Picker in Jetpack Compose?**
> There are two ways: (1) Use Material3's `DatePickerDialog` composable with `rememberDatePickerState()` for a fully Compose-based solution. (2) Use Android's built-in `android.app.DatePickerDialog` which is a traditional dialog shown programmatically. The Material3 approach is preferred in Compose apps.

---

## 3.4 Time Picker Dialog

### Using Material3 TimePicker in Compose

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun TimePickerExample() {
    var showTimePicker by remember { mutableStateOf(false) }
    var selectedTime by remember { mutableStateOf("No time selected") }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text(text = selectedTime, fontSize = 20.sp)

        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = { showTimePicker = true }) {
            Text("Pick a Time")
        }
    }

    if (showTimePicker) {
        val timePickerState = rememberTimePickerState(
            initialHour = 12,
            initialMinute = 0,
            is24Hour = false
        )

        AlertDialog(
            onDismissRequest = { showTimePicker = false },
            title = { Text("Select Time") },
            text = { TimePicker(state = timePickerState) },
            confirmButton = {
                TextButton(onClick = {
                    val hour = timePickerState.hour
                    val minute = timePickerState.minute
                    val amPm = if (hour < 12) "AM" else "PM"
                    val displayHour = if (hour % 12 == 0) 12 else hour % 12
                    selectedTime = String.format("%02d:%02d %s", displayHour, minute, amPm)
                    showTimePicker = false
                }) {
                    Text("OK")
                }
            },
            dismissButton = {
                TextButton(onClick = { showTimePicker = false }) {
                    Text("Cancel")
                }
            }
        )
    }
}
```

### Using Android's Built-in TimePickerDialog

```kotlin
@Composable
fun AndroidTimePickerExample(context: Context) {
    var selectedTime by remember { mutableStateOf("No time selected") }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text(text = selectedTime, fontSize = 20.sp)
        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = {
            val calendar = Calendar.getInstance()
            val hour = calendar.get(Calendar.HOUR_OF_DAY)
            val minute = calendar.get(Calendar.MINUTE)

            TimePickerDialog(
                context,
                { _, selectedHour, selectedMinute ->
                    selectedTime = String.format("%02d:%02d", selectedHour, selectedMinute)
                },
                hour, minute, false  // false = 12-hour format
            ).show()
        }) {
            Text("Pick Time")
        }
    }
}
```

---

## 3.5 Combined Date and Time Picker

```kotlin
@Composable
fun DateTimePickerScreen(context: Context) {
    var date by remember { mutableStateOf("Select Date") }
    var time by remember { mutableStateOf("Select Time") }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        // Date display and picker
        Card(modifier = Modifier.fillMaxWidth()) {
            Row(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(16.dp),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text("Date: $date", fontSize = 18.sp)
                Button(onClick = {
                    val cal = Calendar.getInstance()
                    DatePickerDialog(context, { _, y, m, d ->
                        date = "$d/${m + 1}/$y"
                    }, cal.get(Calendar.YEAR), cal.get(Calendar.MONTH),
                       cal.get(Calendar.DAY_OF_MONTH)).show()
                }) {
                    Text("Pick")
                }
            }
        }

        Spacer(modifier = Modifier.height(16.dp))

        // Time display and picker
        Card(modifier = Modifier.fillMaxWidth()) {
            Row(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(16.dp),
                horizontalArrangement = Arrangement.SpaceBetween,
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text("Time: $time", fontSize = 18.sp)
                Button(onClick = {
                    val cal = Calendar.getInstance()
                    TimePickerDialog(context, { _, h, m ->
                        time = String.format("%02d:%02d", h, m)
                    }, cal.get(Calendar.HOUR_OF_DAY), cal.get(Calendar.MINUTE),
                       false).show()
                }) {
                    Text("Pick")
                }
            }
        }

        Spacer(modifier = Modifier.height(24.dp))

        Text(
            "Selected: $date at $time",
            fontSize = 18.sp,
            fontWeight = FontWeight.Bold
        )
    }
}
```

---

## Viva Questions & Answers

**Q1: What is a Notification Channel and why is it needed?**
> A Notification Channel is a category for grouping notifications. From Android 8.0 (API 26), every notification MUST belong to a channel. Users can independently control settings (sound, vibration, importance) for each channel. Without a channel, notifications won't appear on Android 8.0+.

**Q2: What are the different notification importance levels?**
> `IMPORTANCE_HIGH` (heads-up, sound), `IMPORTANCE_DEFAULT` (sound, no heads-up), `IMPORTANCE_LOW` (no sound), `IMPORTANCE_MIN` (no sound, no visual interruption), `IMPORTANCE_NONE` (blocked).

**Q3: What is the minimum requirement to create a notification?**
> Three things are required: (1) `setSmallIcon()` — an icon, (2) `setContentTitle()` — the title, (3) `setContentText()` — the message text. On Android 8.0+, you also need a notification channel.

**Q4: What permission is needed for notifications on Android 13+?**
> `android.permission.POST_NOTIFICATIONS` — this is a runtime permission that must be requested from the user at runtime starting from Android 13 (API 33).

**Q5: What is `setAutoCancel(true)`?**
> It means the notification will automatically disappear (be dismissed) when the user taps on it.

**Q6: How do you show a DatePickerDialog in Compose?**
> Two approaches: (1) Material3 `DatePickerDialog` composable with `rememberDatePickerState()`, or (2) Android's `android.app.DatePickerDialog` called from a button click. Both let the user select a date and return the result via a callback.

**Q7: What is the difference between DatePicker and TimePickerDialog?**
> DatePicker allows the user to select a date (day/month/year). TimePickerDialog allows the user to select a time (hour/minute). They serve different purposes but are often used together.

**Q8: How do you handle the selected date from DatePickerDialog?**
> The callback receives `(year, month, day)`. Note that month is **0-indexed** (January = 0), so add 1 when displaying: `"$day/${month + 1}/$year"`.

**Q9: What is NotificationCompat.BigTextStyle?**
> A notification style that shows a longer text when the notification is expanded. Initially shows a summary, but when the user pulls down, the full text is revealed. Created using `NotificationCompat.BigTextStyle().bigText("long text")`.

**Q10: Can you update an existing notification?**
> Yes. Call `notify()` with the **same notification ID** and the updated notification builder. The system will replace the existing notification with the new one instead of creating a duplicate.

---
