# Unit 5: Modern Data Storage & Permission Management

---

## Key Definitions (Must Know for Viva)

| Keyword | Definition |
|---|---|
| **DataStore** | A Jetpack data storage solution that stores key-value pairs or typed objects. It replaces SharedPreferences with a safer, asynchronous API using Kotlin coroutines and Flow. |
| **Preferences DataStore** | A type of DataStore that stores simple key-value pairs (like SharedPreferences) but uses coroutines and Flow for asynchronous, safe access. |
| **Proto DataStore** | A type of DataStore that stores typed objects using Protocol Buffers. Provides type safety. |
| **SharedPreferences** | The older Android API for storing key-value pairs. It has issues: synchronous access on UI thread, no type safety, no error handling. DataStore is the recommended replacement. |
| **Flow** | A Kotlin coroutine type that emits values asynchronously over time. DataStore returns `Flow<T>` to observe data changes reactively. |
| **Coroutine** | A lightweight thread in Kotlin for asynchronous programming. Used for non-blocking operations like file I/O, network calls, and DataStore access. |
| **suspend function** | A function that can be paused and resumed without blocking the thread. Marked with the `suspend` keyword. Required for DataStore write operations. |
| **Scoped Storage** | A storage model (introduced in Android 10 / API 29) that restricts app access to external storage. Apps can only access their own app-specific directory and specific media files. |
| **MediaStore** | An API for accessing shared media files (images, videos, audio) on the device in a scoped storage-compliant way. |
| **ContentResolver** | A client object for accessing content providers. Used with MediaStore to query, insert, and delete media files. |
| **SAF (Storage Access Framework)** | A framework that lets users browse and select files/directories through a system file picker. Uses Intents like `ACTION_OPEN_DOCUMENT`. |
| **Runtime Permission** | A permission that must be requested from the user AT RUNTIME (while the app is running), not just declared in the manifest. Required from Android 6.0 (API 23). |
| **Dangerous Permission** | Permissions that access sensitive data (camera, location, contacts, storage). These require runtime permission requests. |
| **Normal Permission** | Permissions that don't access sensitive data (INTERNET, VIBRATE). Automatically granted at install time. |
| **rememberLauncherForActivityResult** | A Compose API that registers a launcher for an activity result (like requesting permissions) and remembers it across recompositions. |
| **ActivityResultContract** | A contract defining the input/output types for activity results. `RequestPermission` and `RequestMultiplePermissions` are common contracts. |
| **shouldShowRequestPermissionRationale** | A method that returns `true` if the user previously denied a permission and the app should explain WHY the permission is needed before requesting again. |
| **getExternalFilesDir()** | Returns the app's private external storage directory. Files here are deleted when the app is uninstalled. No permissions needed. |
| **preferencesKey** | A typed key used to identify values stored in Preferences DataStore. Types: `stringPreferencesKey`, `intPreferencesKey`, `booleanPreferencesKey`. |
| **collectAsState** | A Compose extension function that collects a Flow and converts it into a Compose State, triggering recomposition when the value changes. |

---

## 5.1 DataStore (Preferences DataStore)

### What is DataStore?
DataStore is the modern replacement for SharedPreferences. It provides:
- **Asynchronous** access using Kotlin Coroutines and Flow (no UI blocking)
- **Consistency** with transactional API
- **Error handling** with proper exception handling
- **Type safety** with typed keys

### SharedPreferences vs DataStore:

| Feature | SharedPreferences | Preferences DataStore |
|---|---|---|
| **API** | Synchronous (blocks UI thread) | Asynchronous (coroutines + Flow) |
| **Thread Safety** | Not thread-safe | Thread-safe |
| **Error Handling** | No error signaling | Catches exceptions via Flow |
| **Type Safety** | Runtime errors possible | Typed keys |
| **Data Format** | XML file | Protocol Buffers file |

### Setup — Add Dependency:
```gradle
// build.gradle (Module)
dependencies {
    implementation "androidx.datastore:datastore-preferences:1.1.1"
}
```

### Complete DataStore Example:

```kotlin
// Step 1: Create DataStore instance (top-level, outside class)
val Context.dataStore by preferencesDataStore(name = "user_preferences")

// Step 2: Define keys
object PreferenceKeys {
    val USER_NAME = stringPreferencesKey("user_name")
    val USER_AGE = intPreferencesKey("user_age")
    val IS_DARK_MODE = booleanPreferencesKey("is_dark_mode")
    val IS_LOGGED_IN = booleanPreferencesKey("is_logged_in")
}
```

```kotlin
// Step 3: Write data (suspend function)
suspend fun saveUserName(context: Context, name: String) {
    context.dataStore.edit { preferences ->
        preferences[PreferenceKeys.USER_NAME] = name
    }
}

suspend fun saveUserAge(context: Context, age: Int) {
    context.dataStore.edit { preferences ->
        preferences[PreferenceKeys.USER_AGE] = age
    }
}

suspend fun saveDarkMode(context: Context, isDark: Boolean) {
    context.dataStore.edit { preferences ->
        preferences[PreferenceKeys.IS_DARK_MODE] = isDark
    }
}
```

```kotlin
// Step 4: Read data (returns Flow)
fun getUserName(context: Context): Flow<String> {
    return context.dataStore.data.map { preferences ->
        preferences[PreferenceKeys.USER_NAME] ?: "Guest"
    }
}

fun getUserAge(context: Context): Flow<Int> {
    return context.dataStore.data.map { preferences ->
        preferences[PreferenceKeys.USER_AGE] ?: 0
    }
}

fun getDarkMode(context: Context): Flow<Boolean> {
    return context.dataStore.data.map { preferences ->
        preferences[PreferenceKeys.IS_DARK_MODE] ?: false
    }
}
```

```kotlin
// Step 5: Use in Composable
@Composable
fun DataStoreScreen(context: Context) {
    var name by remember { mutableStateOf("") }
    val scope = rememberCoroutineScope()

    // Read data as State
    val savedName by getUserName(context).collectAsState(initial = "Guest")
    val isDarkMode by getDarkMode(context).collectAsState(initial = false)

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("Saved Name: $savedName", fontSize = 20.sp)

        Spacer(modifier = Modifier.height(16.dp))

        OutlinedTextField(
            value = name,
            onValueChange = { name = it },
            label = { Text("Enter Name") }
        )

        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = {
            scope.launch {
                saveUserName(context, name)  // Save using coroutine
            }
        }) {
            Text("Save Name")
        }

        Spacer(modifier = Modifier.height(24.dp))

        // Dark mode toggle
        Row(verticalAlignment = Alignment.CenterVertically) {
            Text("Dark Mode")
            Spacer(modifier = Modifier.width(8.dp))
            Switch(
                checked = isDarkMode,
                onCheckedChange = { isChecked ->
                    scope.launch {
                        saveDarkMode(context, isChecked)
                    }
                }
            )
        }
    }
}
```

**Viva Q: What is DataStore and why should we use it instead of SharedPreferences?**
> DataStore is a Jetpack library for data storage using key-value pairs or typed objects. It replaces SharedPreferences because: (1) it's asynchronous — won't block the UI thread, (2) it's thread-safe, (3) it has proper error handling via Flow, (4) it uses typed keys. SharedPreferences is synchronous and can cause ANR on the main thread.

**Viva Q: What is `collectAsState`?**
> `collectAsState()` is a Compose extension that collects a Kotlin Flow and converts it into a Compose State. When the Flow emits a new value, it triggers recomposition. The `initial` parameter provides a default value before the first emission.

---

## 5.2 Scoped Storage

### What is Scoped Storage?
Starting from **Android 10 (API 29)**, apps have limited access to external storage:
- Apps can **freely access** their own app-specific directory
- Apps need to use **MediaStore** or **SAF** to access shared files
- Apps can **NO longer** access arbitrary files on external storage

### Storage Locations:

| Location | Access | Persistence | Permission Needed |
|---|---|---|---|
| **Internal Storage** (`filesDir`) | App only | Deleted with app | None |
| **App-specific External** (`getExternalFilesDir()`) | App only | Deleted with app | None |
| **Shared Storage** (Photos, Videos) | All apps via MediaStore | Persists after uninstall | READ_MEDIA_IMAGES (API 33+) |
| **SAF** (any file) | User-selected files | Varies | None (user picks file) |

### App-Specific Storage:

```kotlin
// Write to internal storage
fun writeToInternalStorage(context: Context, filename: String, content: String) {
    context.openFileOutput(filename, Context.MODE_PRIVATE).use { stream ->
        stream.write(content.toByteArray())
    }
}

// Read from internal storage
fun readFromInternalStorage(context: Context, filename: String): String {
    return context.openFileInput(filename).bufferedReader().readText()
}
```

### App-Specific External Storage:

```kotlin
// Write to app-specific external storage
fun writeToExternalStorage(context: Context, filename: String, content: String) {
    val file = File(context.getExternalFilesDir(null), filename)
    file.writeText(content)
}

// Read from app-specific external storage
fun readFromExternalStorage(context: Context, filename: String): String {
    val file = File(context.getExternalFilesDir(null), filename)
    return file.readText()
}
```

### Using SAF (Storage Access Framework) to Pick a File:

```kotlin
@Composable
fun FilePickerScreen() {
    var fileContent by remember { mutableStateOf("No file selected") }
    val context = LocalContext.current

    // Register file picker launcher
    val filePickerLauncher = rememberLauncherForActivityResult(
        contract = ActivityResultContracts.OpenDocument()
    ) { uri: Uri? ->
        uri?.let {
            // Read file content
            context.contentResolver.openInputStream(it)?.use { stream ->
                fileContent = stream.bufferedReader().readText()
            }
        }
    }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Button(onClick = {
            filePickerLauncher.launch(arrayOf("text/*"))  // Only text files
        }) {
            Text("Pick a File")
        }

        Spacer(modifier = Modifier.height(16.dp))

        Text(fileContent)
    }
}
```

**Viva Q: What is Scoped Storage?**
> Scoped Storage (Android 10+) restricts app access to the file system. Apps can freely access their own app-specific directories but must use MediaStore API or Storage Access Framework (SAF) to access shared media files. This improves user privacy and security.

---

## 5.3 Runtime Permissions with Compose UI

### What are Runtime Permissions?
From Android 6.0 (API 23), **dangerous permissions** must be requested at runtime. The user can grant or deny them.

### Permission Types:

| Type | Example | When Granted |
|---|---|---|
| **Normal** | INTERNET, VIBRATE, ACCESS_WIFI_STATE | Automatically at install |
| **Dangerous** | CAMERA, READ_CONTACTS, ACCESS_FINE_LOCATION | User must approve at runtime |

### Single Permission Request:

```kotlin
@Composable
fun CameraPermissionScreen() {
    val context = LocalContext.current
    var hasPermission by remember {
        mutableStateOf(
            ContextCompat.checkSelfPermission(
                context, Manifest.permission.CAMERA
            ) == PackageManager.PERMISSION_GRANTED
        )
    }

    // Permission launcher
    val permissionLauncher = rememberLauncherForActivityResult(
        contract = ActivityResultContracts.RequestPermission()
    ) { isGranted ->
        hasPermission = isGranted
        if (isGranted) {
            Toast.makeText(context, "Camera Permission Granted!", Toast.LENGTH_SHORT).show()
        } else {
            Toast.makeText(context, "Camera Permission Denied!", Toast.LENGTH_SHORT).show()
        }
    }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        if (hasPermission) {
            Text("✅ Camera Permission Granted", fontSize = 20.sp, color = Color.Green)
            // Show camera UI here
        } else {
            Text("❌ Camera Permission Not Granted", fontSize = 20.sp, color = Color.Red)

            Spacer(modifier = Modifier.height(16.dp))

            Button(onClick = {
                permissionLauncher.launch(Manifest.permission.CAMERA)
            }) {
                Text("Request Camera Permission")
            }
        }
    }
}
```

### Multiple Permissions Request:

```kotlin
@Composable
fun MultiplePermissionsScreen() {
    val context = LocalContext.current
    var permissionStatus by remember { mutableStateOf("Not checked") }

    val multiPermissionLauncher = rememberLauncherForActivityResult(
        contract = ActivityResultContracts.RequestMultiplePermissions()
    ) { permissions ->
        val allGranted = permissions.values.all { it }
        permissionStatus = if (allGranted) {
            "All permissions granted ✅"
        } else {
            val denied = permissions.filter { !it.value }.keys
            "Denied: ${denied.joinToString()}"
        }
    }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text(permissionStatus, fontSize = 18.sp)

        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = {
            multiPermissionLauncher.launch(
                arrayOf(
                    Manifest.permission.CAMERA,
                    Manifest.permission.ACCESS_FINE_LOCATION,
                    Manifest.permission.RECORD_AUDIO
                )
            )
        }) {
            Text("Request All Permissions")
        }
    }
}
```

> **Don't forget AndroidManifest.xml permissions:**
```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

### Permission with Rationale:

```kotlin
@Composable
fun PermissionWithRationale(activity: ComponentActivity) {
    var showRationale by remember { mutableStateOf(false) }

    val permissionLauncher = rememberLauncherForActivityResult(
        contract = ActivityResultContracts.RequestPermission()
    ) { isGranted ->
        if (!isGranted) {
            // Check if we should show rationale
            showRationale = activity.shouldShowRequestPermissionRationale(
                Manifest.permission.CAMERA
            )
        }
    }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Button(onClick = {
            permissionLauncher.launch(Manifest.permission.CAMERA)
        }) {
            Text("Request Permission")
        }

        if (showRationale) {
            Spacer(modifier = Modifier.height(16.dp))
            AlertDialog(
                onDismissRequest = { showRationale = false },
                title = { Text("Permission Needed") },
                text = { Text("Camera permission is required to take photos. Please grant it.") },
                confirmButton = {
                    TextButton(onClick = {
                        showRationale = false
                        permissionLauncher.launch(Manifest.permission.CAMERA)
                    }) {
                        Text("Grant")
                    }
                },
                dismissButton = {
                    TextButton(onClick = { showRationale = false }) {
                        Text("Cancel")
                    }
                }
            )
        }
    }
}
```

**Viva Q: What is a Runtime Permission?**
> A runtime permission is a permission that must be explicitly requested from the user while the app is running. Introduced in Android 6.0 (API 23). The user sees a dialog and can grant or deny. Example: CAMERA, LOCATION, CONTACTS. Normal permissions like INTERNET are automatically granted.

**Viva Q: What is `rememberLauncherForActivityResult`?**
> It's a Compose API that registers a callback to handle the result of an Activity (like permission request or file picker). It takes an `ActivityResultContract` (defines input/output types) and a callback lambda. It remembers the launcher across recompositions.

---

## Viva Questions & Answers

**Q1: What is the difference between SharedPreferences and DataStore?**
> SharedPreferences is synchronous (blocks UI thread), not type-safe, and can cause ANR. DataStore is asynchronous (uses coroutines + Flow), type-safe, and handles errors properly. DataStore is the recommended replacement.

**Q2: What is a Flow in Kotlin?**
> A Flow is a cold asynchronous stream that emits values over time. It's used in DataStore to observe data changes reactively. You collect a Flow using `.collect()` or in Compose using `.collectAsState()`.

**Q3: What is `preferencesDataStore`?**
> A delegate property that creates a singleton DataStore instance using the given name. It should be declared at the top level (file level) to ensure only one instance exists: `val Context.dataStore by preferencesDataStore(name = "settings")`.

**Q4: What is Scoped Storage and why was it introduced?**
> Scoped Storage (Android 10+) restricts apps from accessing arbitrary files on external storage. Each app can only access its own app-specific directory. To access shared media, use MediaStore. This was introduced for **user privacy and security** — apps can no longer read other apps' files or snoop on user data.

**Q5: What is the difference between Normal and Dangerous permissions?**
> Normal permissions (INTERNET, VIBRATE) are automatically granted at install — they don't access sensitive data. Dangerous permissions (CAMERA, LOCATION, CONTACTS) access sensitive data and must be requested from the user at runtime.

**Q6: What happens if a user denies a permission permanently (Don't ask again)?**
> If the user selects "Don't ask again," `shouldShowRequestPermissionRationale()` returns false, and you can no longer show the permission dialog. You should direct the user to the app's Settings page to manually grant the permission.

**Q7: What is `getExternalFilesDir()`?**
> It returns the app-specific directory on external storage (`/Android/data/your.package/files/`). Files here are private to the app, require no permissions, and are deleted when the app is uninstalled.

**Q8: What is MediaStore?**
> MediaStore is an API for accessing shared media files (images, videos, audio) on the device. It provides a content provider interface. With Scoped Storage, it's the proper way to access media files without direct file path access.

---
