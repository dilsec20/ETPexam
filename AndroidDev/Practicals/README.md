# Android Development Practicals — Complete Code

---

## Practical 1: Application Based on Different Views & Components

### App: Student List with Grid, Spinner, Rating, and Progress Bar

```kotlin
// MainActivity.kt
package com.example.viewscomponents

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.background
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.grid.GridCells
import androidx.compose.foundation.lazy.grid.LazyVerticalGrid
import androidx.compose.foundation.lazy.grid.items
import androidx.compose.foundation.lazy.items
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.*
import androidx.compose.material.icons.outlined.Star
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Brush
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MaterialTheme {
                ViewsComponentsApp()
            }
        }
    }
}

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun ViewsComponentsApp() {
    var selectedTab by remember { mutableStateOf(0) }
    val tabs = listOf("List", "Grid", "Spinner", "Rating", "Progress")

    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("Views & Components") },
                colors = TopAppBarDefaults.topAppBarColors(
                    containerColor = Color(0xFF6200EE),
                    titleContentColor = Color.White
                )
            )
        }
    ) { padding ->
        Column(modifier = Modifier.padding(padding)) {
            ScrollableTabRow(selectedTabIndex = selectedTab) {
                tabs.forEachIndexed { index, title ->
                    Tab(
                        selected = selectedTab == index,
                        onClick = { selectedTab = index },
                        text = { Text(title) }
                    )
                }
            }

            when (selectedTab) {
                0 -> StudentListScreen()
                1 -> PhotoGridScreen()
                2 -> SpinnerScreen()
                3 -> RatingScreen()
                4 -> ProgressScreen()
            }
        }
    }
}

// -------- LIST SCREEN --------
@Composable
fun StudentListScreen() {
    val students = listOf(
        "Amit Sharma", "Priya Patel", "Rahul Kumar",
        "Sneha Gupta", "Vijay Singh", "Neha Verma",
        "Arjun Reddy", "Kavita Nair", "Rohit Joshi"
    )

    LazyColumn(
        contentPadding = PaddingValues(16.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        items(students) { student ->
            Card(
                modifier = Modifier.fillMaxWidth(),
                elevation = CardDefaults.cardElevation(4.dp),
                shape = RoundedCornerShape(12.dp)
            ) {
                Row(
                    modifier = Modifier.padding(16.dp),
                    verticalAlignment = Alignment.CenterVertically
                ) {
                    Icon(
                        Icons.Default.Person,
                        contentDescription = null,
                        tint = Color(0xFF6200EE),
                        modifier = Modifier.size(40.dp)
                    )
                    Spacer(modifier = Modifier.width(16.dp))
                    Text(text = student, fontSize = 18.sp)
                }
            }
        }
    }
}

// -------- GRID SCREEN --------
@Composable
fun PhotoGridScreen() {
    val colors = listOf(
        Color(0xFFE91E63), Color(0xFF9C27B0), Color(0xFF673AB7),
        Color(0xFF3F51B5), Color(0xFF2196F3), Color(0xFF00BCD4),
        Color(0xFF4CAF50), Color(0xFFFF9800), Color(0xFFF44336)
    )

    LazyVerticalGrid(
        columns = GridCells.Fixed(3),
        contentPadding = PaddingValues(8.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp),
        horizontalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        items(colors) { color ->
            Card(
                modifier = Modifier.aspectRatio(1f),
                shape = RoundedCornerShape(12.dp),
                colors = CardDefaults.cardColors(containerColor = color)
            ) {
                Box(contentAlignment = Alignment.Center, modifier = Modifier.fillMaxSize()) {
                    Text("Item", color = Color.White, fontWeight = FontWeight.Bold)
                }
            }
        }
    }
}

// -------- SPINNER SCREEN --------
@Composable
fun SpinnerScreen() {
    var expanded by remember { mutableStateOf(false) }
    var selectedCity by remember { mutableStateOf("Select City") }
    val cities = listOf("Delhi", "Mumbai", "Bangalore", "Chennai", "Kolkata", "Hyderabad")

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("Select Your City", fontSize = 20.sp, fontWeight = FontWeight.Bold)
        Spacer(modifier = Modifier.height(16.dp))

        Box {
            OutlinedButton(onClick = { expanded = true }) {
                Text(selectedCity)
                Icon(Icons.Default.ArrowDropDown, contentDescription = null)
            }
            DropdownMenu(expanded = expanded, onDismissRequest = { expanded = false }) {
                cities.forEach { city ->
                    DropdownMenuItem(
                        text = { Text(city) },
                        onClick = {
                            selectedCity = city
                            expanded = false
                        }
                    )
                }
            }
        }

        Spacer(modifier = Modifier.height(24.dp))
        if (selectedCity != "Select City") {
            Text("You selected: $selectedCity", fontSize = 18.sp, color = Color(0xFF6200EE))
        }
    }
}

// -------- RATING SCREEN --------
@Composable
fun RatingScreen() {
    var rating by remember { mutableStateOf(0) }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("Rate Our App", fontSize = 24.sp, fontWeight = FontWeight.Bold)
        Spacer(modifier = Modifier.height(24.dp))

        // Custom Rating Bar
        Row {
            for (i in 1..5) {
                Icon(
                    imageVector = if (i <= rating) Icons.Filled.Star else Icons.Outlined.Star,
                    contentDescription = "Star $i",
                    tint = if (i <= rating) Color(0xFFFFD700) else Color.Gray,
                    modifier = Modifier
                        .size(48.dp)
                        .clickable { rating = i }
                )
            }
        }

        Spacer(modifier = Modifier.height(16.dp))
        Text("Rating: $rating / 5", fontSize = 18.sp)

        Spacer(modifier = Modifier.height(8.dp))
        Text(
            when (rating) {
                1 -> "😞 Poor"
                2 -> "😐 Fair"
                3 -> "🙂 Good"
                4 -> "😊 Very Good"
                5 -> "🤩 Excellent!"
                else -> "Tap a star to rate"
            },
            fontSize = 20.sp
        )
    }
}

// -------- PROGRESS SCREEN --------
@Composable
fun ProgressScreen() {
    var progress by remember { mutableStateOf(0f) }
    var isLoading by remember { mutableStateOf(false) }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        // Linear Progress Bar (Determinate)
        Text("Download Progress: ${(progress * 100).toInt()}%", fontSize = 18.sp)
        Spacer(modifier = Modifier.height(8.dp))
        LinearProgressIndicator(
            progress = progress,
            modifier = Modifier.fillMaxWidth().height(10.dp),
            color = Color(0xFF6200EE),
            trackColor = Color.LightGray
        )

        Spacer(modifier = Modifier.height(16.dp))

        Row(horizontalArrangement = Arrangement.spacedBy(8.dp)) {
            Button(onClick = { if (progress < 1f) progress += 0.1f }) {
                Text("+10%")
            }
            Button(onClick = { progress = 0f }) {
                Text("Reset")
            }
        }

        Spacer(modifier = Modifier.height(40.dp))

        // Circular Progress Bar (Indeterminate)
        Button(onClick = { isLoading = !isLoading }) {
            Text(if (isLoading) "Stop Loading" else "Start Loading")
        }
        Spacer(modifier = Modifier.height(16.dp))
        if (isLoading) {
            CircularProgressIndicator(
                modifier = Modifier.size(64.dp),
                color = Color(0xFF6200EE),
                strokeWidth = 6.dp
            )
        }
    }
}
```

---

## Practical 2: Application Based on Intents & Different Schedulers

### App: Intent Demo + Alarm Scheduler

```kotlin
// MainActivity.kt
package com.example.intentscheduler

import android.app.AlarmManager
import android.app.PendingIntent
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.net.Uri
import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MaterialTheme {
                IntentSchedulerApp()
            }
        }
    }
}

@Composable
fun IntentSchedulerApp() {
    val context = LocalContext.current
    var name by remember { mutableStateOf("") }

    Column(
        modifier = Modifier.fillMaxSize().padding(24.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.spacedBy(12.dp, Alignment.CenterVertically)
    ) {
        Text("Intent & Scheduler Demo", fontSize = 24.sp)

        Spacer(modifier = Modifier.height(8.dp))

        // --- EXPLICIT INTENT ---
        OutlinedTextField(
            value = name,
            onValueChange = { name = it },
            label = { Text("Enter your name") },
            modifier = Modifier.fillMaxWidth()
        )

        Button(
            onClick = {
                val intent = Intent(context, SecondActivity::class.java)
                intent.putExtra("USER_NAME", name)
                context.startActivity(intent)
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Explicit Intent → SecondActivity")
        }

        Divider()

        // --- IMPLICIT INTENTS ---
        Button(
            onClick = {
                val intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com"))
                context.startActivity(intent)
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Open Website (Implicit)")
        }

        Button(
            onClick = {
                val intent = Intent(Intent.ACTION_DIAL, Uri.parse("tel:9876543210"))
                context.startActivity(intent)
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Dial Number (Implicit)")
        }

        Button(
            onClick = {
                val intent = Intent(Intent.ACTION_SEND).apply {
                    type = "text/plain"
                    putExtra(Intent.EXTRA_TEXT, "Hello from my app!")
                }
                context.startActivity(Intent.createChooser(intent, "Share via"))
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Share Text (Implicit)")
        }

        Divider()

        // --- ALARM MANAGER ---
        Button(
            onClick = {
                val alarmManager = context.getSystemService(Context.ALARM_SERVICE) as AlarmManager
                val intent = Intent(context, AlarmReceiver::class.java)
                val pendingIntent = PendingIntent.getBroadcast(
                    context, 0, intent, PendingIntent.FLAG_IMMUTABLE
                )
                val triggerTime = System.currentTimeMillis() + 10_000
                alarmManager.setExact(AlarmManager.RTC_WAKEUP, triggerTime, pendingIntent)
                Toast.makeText(context, "Alarm set for 10 seconds!", Toast.LENGTH_SHORT).show()
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Set Alarm (10 seconds)")
        }
    }
}
```

```kotlin
// SecondActivity.kt
package com.example.intentscheduler

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

class SecondActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val userName = intent.getStringExtra("USER_NAME") ?: "Unknown"
        setContent {
            MaterialTheme {
                Box(
                    modifier = Modifier.fillMaxSize(),
                    contentAlignment = Alignment.Center
                ) {
                    Column(horizontalAlignment = Alignment.CenterHorizontally) {
                        Text("Welcome!", fontSize = 32.sp)
                        Spacer(modifier = Modifier.height(16.dp))
                        Text("Hello, $userName!", fontSize = 24.sp)
                    }
                }
            }
        }
    }
}
```

```kotlin
// AlarmReceiver.kt
package com.example.intentscheduler

import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.widget.Toast

class AlarmReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        Toast.makeText(context, "⏰ Alarm Triggered!", Toast.LENGTH_LONG).show()
    }
}
```

```xml
<!-- AndroidManifest.xml additions -->
<activity android:name=".SecondActivity" />
<receiver android:name=".AlarmReceiver" android:exported="false" />
```

---

## Practical 3: Application to Implement Custom Views

### App: Custom Styled Login Form

```kotlin
// MainActivity.kt
package com.example.customviews

import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.background
import androidx.compose.foundation.border
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.text.BasicTextField
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.draw.shadow
import androidx.compose.ui.graphics.Brush
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.graphics.vector.ImageVector
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.input.PasswordVisualTransformation
import androidx.compose.ui.text.input.VisualTransformation
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MaterialTheme { CustomLoginScreen() }
        }
    }
}

// Custom Text Composable
@Composable
fun AppTitle(text: String, color: Color = Color(0xFF6200EE)) {
    Text(
        text = text,
        fontSize = 32.sp,
        fontWeight = FontWeight.Bold,
        color = color
    )
}

// Custom TextField Composable
@Composable
fun CustomTextField(
    value: String,
    onValueChange: (String) -> Unit,
    label: String,
    icon: ImageVector,
    isPassword: Boolean = false
) {
    OutlinedTextField(
        value = value,
        onValueChange = onValueChange,
        label = { Text(label) },
        leadingIcon = { Icon(icon, contentDescription = null) },
        visualTransformation = if (isPassword) PasswordVisualTransformation()
                               else VisualTransformation.None,
        shape = RoundedCornerShape(16.dp),
        modifier = Modifier.fillMaxWidth(),
        colors = OutlinedTextFieldDefaults.colors(
            focusedBorderColor = Color(0xFF6200EE),
            focusedLabelColor = Color(0xFF6200EE)
        ),
        singleLine = true
    )
}

// Custom Button Composable
@Composable
fun GradientButton(text: String, onClick: () -> Unit) {
    Button(
        onClick = onClick,
        modifier = Modifier
            .fillMaxWidth()
            .height(56.dp),
        shape = RoundedCornerShape(16.dp),
        colors = ButtonDefaults.buttonColors(
            containerColor = Color(0xFF6200EE)
        ),
        elevation = ButtonDefaults.buttonElevation(8.dp)
    ) {
        Text(text, fontSize = 18.sp, fontWeight = FontWeight.Bold)
    }
}

@Composable
fun CustomLoginScreen() {
    val context = LocalContext.current
    var email by remember { mutableStateOf("") }
    var password by remember { mutableStateOf("") }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        // Custom circular avatar
        Box(
            modifier = Modifier
                .size(100.dp)
                .clip(CircleShape)
                .background(Color(0xFF6200EE)),
            contentAlignment = Alignment.Center
        ) {
            Icon(
                Icons.Default.Person,
                contentDescription = null,
                tint = Color.White,
                modifier = Modifier.size(60.dp)
            )
        }

        Spacer(modifier = Modifier.height(24.dp))
        AppTitle(text = "Welcome Back")
        Spacer(modifier = Modifier.height(32.dp))

        CustomTextField(
            value = email,
            onValueChange = { email = it },
            label = "Email",
            icon = Icons.Default.Email
        )

        Spacer(modifier = Modifier.height(16.dp))

        CustomTextField(
            value = password,
            onValueChange = { password = it },
            label = "Password",
            icon = Icons.Default.Lock,
            isPassword = true
        )

        Spacer(modifier = Modifier.height(24.dp))

        GradientButton(text = "Login") {
            Toast.makeText(context, "Login: $email", Toast.LENGTH_SHORT).show()
        }

        Spacer(modifier = Modifier.height(16.dp))
        TextButton(onClick = { }) {
            Text("Forgot Password?", color = Color(0xFF6200EE))
        }
    }
}
```

---

## Practical 4: Application Based on Different Storage Options

### App: DataStore Preferences — Save/Load User Settings

```kotlin
// MainActivity.kt
package com.example.storagedemo

import android.content.Context
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.datastore.preferences.core.booleanPreferencesKey
import androidx.datastore.preferences.core.edit
import androidx.datastore.preferences.core.stringPreferencesKey
import androidx.datastore.preferences.preferencesDataStore
import kotlinx.coroutines.flow.Flow
import kotlinx.coroutines.flow.map
import kotlinx.coroutines.launch

// Create DataStore
val Context.dataStore by preferencesDataStore(name = "user_settings")

// Keys
object PrefKeys {
    val USER_NAME = stringPreferencesKey("user_name")
    val DARK_MODE = booleanPreferencesKey("dark_mode")
}

// Save functions
suspend fun saveName(context: Context, name: String) {
    context.dataStore.edit { it[PrefKeys.USER_NAME] = name }
}

suspend fun saveDarkMode(context: Context, isDark: Boolean) {
    context.dataStore.edit { it[PrefKeys.DARK_MODE] = isDark }
}

// Read functions
fun getName(context: Context): Flow<String> =
    context.dataStore.data.map { it[PrefKeys.USER_NAME] ?: "Guest" }

fun getDarkMode(context: Context): Flow<Boolean> =
    context.dataStore.data.map { it[PrefKeys.DARK_MODE] ?: false }

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent { MaterialTheme { StorageDemoScreen() } }
    }
}

@Composable
fun StorageDemoScreen() {
    val context = LocalContext.current
    val scope = rememberCoroutineScope()
    var nameInput by remember { mutableStateOf("") }

    val savedName by getName(context).collectAsState(initial = "Guest")
    val isDarkMode by getDarkMode(context).collectAsState(initial = false)

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("DataStore Demo", fontSize = 28.sp, fontWeight = FontWeight.Bold)
        Spacer(modifier = Modifier.height(24.dp))

        Text("Hello, $savedName!", fontSize = 22.sp)
        Spacer(modifier = Modifier.height(16.dp))

        OutlinedTextField(
            value = nameInput,
            onValueChange = { nameInput = it },
            label = { Text("Enter Name") },
            modifier = Modifier.fillMaxWidth()
        )
        Spacer(modifier = Modifier.height(12.dp))

        Button(
            onClick = { scope.launch { saveName(context, nameInput) } },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Save Name")
        }

        Spacer(modifier = Modifier.height(24.dp))

        Row(
            modifier = Modifier.fillMaxWidth(),
            horizontalArrangement = Arrangement.SpaceBetween,
            verticalAlignment = Alignment.CenterVertically
        ) {
            Text("Dark Mode", fontSize = 18.sp)
            Switch(
                checked = isDarkMode,
                onCheckedChange = { scope.launch { saveDarkMode(context, it) } }
            )
        }

        Spacer(modifier = Modifier.height(8.dp))
        Text(
            "Dark Mode is ${if (isDarkMode) "ON" else "OFF"}",
            fontSize = 16.sp
        )
    }
}
```

---

## Practical 5: Application to Implement Different Types of Navigation

### App: Tabs + Drawer + Pager Navigation

```kotlin
// MainActivity.kt
package com.example.navigationdemo

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.ExperimentalFoundationApi
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.pager.HorizontalPager
import androidx.compose.foundation.pager.rememberPagerState
import androidx.compose.foundation.shape.CircleShape
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import kotlinx.coroutines.launch

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent { MaterialTheme { NavigationApp() } }
    }
}

@OptIn(ExperimentalMaterial3Api::class, ExperimentalFoundationApi::class)
@Composable
fun NavigationApp() {
    val drawerState = rememberDrawerState(DrawerValue.Closed)
    val scope = rememberCoroutineScope()
    var selectedDrawerItem by remember { mutableStateOf("Home") }

    val tabs = listOf("Feed", "Search", "Profile")
    val pagerState = rememberPagerState(pageCount = { tabs.size })

    ModalNavigationDrawer(
        drawerState = drawerState,
        drawerContent = {
            ModalDrawerSheet {
                // Drawer Header
                Box(
                    modifier = Modifier
                        .fillMaxWidth()
                        .height(120.dp)
                        .background(Color(0xFF6200EE)),
                    contentAlignment = Alignment.Center
                ) {
                    Text("My App", color = Color.White, fontSize = 24.sp,
                         fontWeight = FontWeight.Bold)
                }

                Spacer(modifier = Modifier.height(8.dp))

                listOf(
                    "Home" to Icons.Default.Home,
                    "Settings" to Icons.Default.Settings,
                    "About" to Icons.Default.Info
                ).forEach { (label, icon) ->
                    NavigationDrawerItem(
                        icon = { Icon(icon, contentDescription = null) },
                        label = { Text(label) },
                        selected = selectedDrawerItem == label,
                        onClick = {
                            selectedDrawerItem = label
                            scope.launch { drawerState.close() }
                        },
                        modifier = Modifier.padding(horizontal = 12.dp)
                    )
                }
            }
        }
    ) {
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text(selectedDrawerItem) },
                    navigationIcon = {
                        IconButton(onClick = { scope.launch { drawerState.open() } }) {
                            Icon(Icons.Default.Menu, contentDescription = "Menu")
                        }
                    },
                    colors = TopAppBarDefaults.topAppBarColors(
                        containerColor = Color(0xFF6200EE),
                        titleContentColor = Color.White,
                        navigationIconContentColor = Color.White
                    )
                )
            }
        ) { padding ->
            Column(modifier = Modifier.padding(padding)) {
                // TabRow
                TabRow(selectedTabIndex = pagerState.currentPage) {
                    tabs.forEachIndexed { index, title ->
                        Tab(
                            selected = pagerState.currentPage == index,
                            onClick = { scope.launch { pagerState.animateScrollToPage(index) } },
                            text = { Text(title) }
                        )
                    }
                }

                // HorizontalPager
                HorizontalPager(state = pagerState, modifier = Modifier.fillMaxSize()) { page ->
                    Box(
                        modifier = Modifier.fillMaxSize(),
                        contentAlignment = Alignment.Center
                    ) {
                        Text("${tabs[page]} Screen", fontSize = 28.sp, fontWeight = FontWeight.Bold)
                    }
                }
            }
        }
    }
}
```

---

## Practical 6: Notification Implementation

### App: Notifications with Multiple Channels

```kotlin
// MainActivity.kt
package com.example.notificationdemo

import android.app.NotificationChannel
import android.app.NotificationManager
import android.app.PendingIntent
import android.content.Context
import android.content.Intent
import android.os.Build
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.core.app.NotificationCompat
import androidx.core.app.NotificationManagerCompat

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        createChannels()
        setContent { MaterialTheme { NotificationScreen() } }
    }

    private fun createChannels() {
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            val manager = getSystemService(NotificationManager::class.java)

            val high = NotificationChannel(
                "high_channel", "Important",
                NotificationManager.IMPORTANCE_HIGH
            ).apply { description = "High priority notifications" }

            val low = NotificationChannel(
                "low_channel", "Updates",
                NotificationManager.IMPORTANCE_LOW
            ).apply { description = "Low priority updates" }

            manager.createNotificationChannel(high)
            manager.createNotificationChannel(low)
        }
    }
}

@Composable
fun NotificationScreen() {
    val context = LocalContext.current

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.spacedBy(16.dp, Alignment.CenterVertically)
    ) {
        Text("Notification Demo", fontSize = 28.sp, fontWeight = FontWeight.Bold)

        Button(onClick = {
            val intent = Intent(context, MainActivity::class.java)
            val pending = PendingIntent.getActivity(
                context, 0, intent, PendingIntent.FLAG_IMMUTABLE
            )
            val notification = NotificationCompat.Builder(context, "high_channel")
                .setSmallIcon(android.R.drawable.ic_dialog_info)
                .setContentTitle("New Message!")
                .setContentText("You have a new message from Amit")
                .setPriority(NotificationCompat.PRIORITY_HIGH)
                .setContentIntent(pending)
                .setAutoCancel(true)
                .build()
            NotificationManagerCompat.from(context).notify(1, notification)
        }, modifier = Modifier.fillMaxWidth()) {
            Text("Simple Notification")
        }

        Button(onClick = {
            val notification = NotificationCompat.Builder(context, "high_channel")
                .setSmallIcon(android.R.drawable.ic_dialog_info)
                .setContentTitle("Long Message")
                .setStyle(NotificationCompat.BigTextStyle()
                    .bigText("This is a long notification that expands when " +
                             "the user pulls it down. It can show much more " +
                             "text than a regular notification."))
                .setAutoCancel(true)
                .build()
            NotificationManagerCompat.from(context).notify(2, notification)
        }, modifier = Modifier.fillMaxWidth()) {
            Text("Big Text Notification")
        }

        Button(onClick = {
            val notification = NotificationCompat.Builder(context, "low_channel")
                .setSmallIcon(android.R.drawable.ic_dialog_info)
                .setContentTitle("App Update")
                .setContentText("Version 2.0 is now available")
                .setPriority(NotificationCompat.PRIORITY_LOW)
                .setAutoCancel(true)
                .build()
            NotificationManagerCompat.from(context).notify(3, notification)
        }, modifier = Modifier.fillMaxWidth()) {
            Text("Low Priority Notification")
        }
    }
}
```

---

## Practical 7: Splash Screen with LaunchedEffect

```kotlin
// SplashActivity.kt
package com.example.splashdemo

import android.content.Intent
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Star
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Brush
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import kotlinx.coroutines.delay

class SplashActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            SplashScreen {
                startActivity(Intent(this, MainActivity::class.java))
                finish()
            }
        }
    }
}

@Composable
fun SplashScreen(onNavigate: () -> Unit) {
    LaunchedEffect(key1 = true) {
        delay(3000L)
        onNavigate()
    }

    Box(
        modifier = Modifier
            .fillMaxSize()
            .background(
                Brush.verticalGradient(
                    listOf(Color(0xFF6200EE), Color(0xFF3700B3))
                )
            ),
        contentAlignment = Alignment.Center
    ) {
        Column(horizontalAlignment = Alignment.CenterHorizontally) {
            Icon(
                Icons.Default.Star,
                contentDescription = null,
                tint = Color.White,
                modifier = Modifier.size(100.dp)
            )
            Spacer(modifier = Modifier.height(16.dp))
            Text("My App", color = Color.White, fontSize = 36.sp,
                 fontWeight = FontWeight.Bold)
            Spacer(modifier = Modifier.height(24.dp))
            CircularProgressIndicator(color = Color.White)
        }
    }
}
```

---

## Practical 8: Date & Time Picker

```kotlin
// MainActivity.kt
package com.example.datetimepicker

import android.app.DatePickerDialog
import android.app.TimePickerDialog
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import java.util.Calendar

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent { MaterialTheme { DateTimeScreen() } }
    }
}

@Composable
fun DateTimeScreen() {
    val context = LocalContext.current
    var selectedDate by remember { mutableStateOf("No date selected") }
    var selectedTime by remember { mutableStateOf("No time selected") }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("Date & Time Picker", fontSize = 28.sp, fontWeight = FontWeight.Bold)

        Spacer(modifier = Modifier.height(32.dp))

        // DATE PICKER
        Card(modifier = Modifier.fillMaxWidth()) {
            Column(modifier = Modifier.padding(16.dp)) {
                Text("Selected Date:", fontWeight = FontWeight.Bold)
                Text(selectedDate, fontSize = 20.sp)
                Spacer(modifier = Modifier.height(8.dp))
                Button(onClick = {
                    val cal = Calendar.getInstance()
                    DatePickerDialog(context, { _, y, m, d ->
                        selectedDate = "$d/${m + 1}/$y"
                    }, cal.get(Calendar.YEAR), cal.get(Calendar.MONTH),
                       cal.get(Calendar.DAY_OF_MONTH)).show()
                }) { Text("Pick Date") }
            }
        }

        Spacer(modifier = Modifier.height(16.dp))

        // TIME PICKER
        Card(modifier = Modifier.fillMaxWidth()) {
            Column(modifier = Modifier.padding(16.dp)) {
                Text("Selected Time:", fontWeight = FontWeight.Bold)
                Text(selectedTime, fontSize = 20.sp)
                Spacer(modifier = Modifier.height(8.dp))
                Button(onClick = {
                    val cal = Calendar.getInstance()
                    TimePickerDialog(context, { _, h, m ->
                        selectedTime = String.format("%02d:%02d", h, m)
                    }, cal.get(Calendar.HOUR_OF_DAY),
                       cal.get(Calendar.MINUTE), false).show()
                }) { Text("Pick Time") }
            }
        }

        Spacer(modifier = Modifier.height(24.dp))
        Text("Appointment: $selectedDate at $selectedTime", fontSize = 16.sp)
    }
}
```

---

## Practical 9: Runtime Permissions

```kotlin
// MainActivity.kt
package com.example.permissiondemo

import android.Manifest
import android.content.pm.PackageManager
import android.os.Bundle
import android.widget.Toast
import androidx.activity.ComponentActivity
import androidx.activity.compose.rememberLauncherForActivityResult
import androidx.activity.compose.setContent
import androidx.activity.result.contract.ActivityResultContracts
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.core.content.ContextCompat

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent { MaterialTheme { PermissionScreen() } }
    }
}

@Composable
fun PermissionScreen() {
    val context = LocalContext.current
    var cameraGranted by remember {
        mutableStateOf(
            ContextCompat.checkSelfPermission(context, Manifest.permission.CAMERA)
                    == PackageManager.PERMISSION_GRANTED
        )
    }

    val launcher = rememberLauncherForActivityResult(
        contract = ActivityResultContracts.RequestPermission()
    ) { granted ->
        cameraGranted = granted
        val msg = if (granted) "Camera Permission Granted!" else "Camera Permission Denied!"
        Toast.makeText(context, msg, Toast.LENGTH_SHORT).show()
    }

    Column(
        modifier = Modifier.fillMaxSize().padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("Permission Demo", fontSize = 28.sp, fontWeight = FontWeight.Bold)
        Spacer(modifier = Modifier.height(24.dp))

        Text(
            if (cameraGranted) "✅ Camera Permission GRANTED" else "❌ Camera Permission DENIED",
            fontSize = 20.sp,
            color = if (cameraGranted) Color.Green else Color.Red
        )

        Spacer(modifier = Modifier.height(16.dp))

        if (!cameraGranted) {
            Button(onClick = {
                launcher.launch(Manifest.permission.CAMERA)
            }) {
                Text("Request Camera Permission")
            }
        }
    }
}
```

```xml
<!-- AndroidManifest.xml -->
<uses-permission android:name="android.permission.CAMERA" />
```

---

## Practical 10: NavHost Navigation

```kotlin
// MainActivity.kt
package com.example.navdemo

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent { MaterialTheme { AppNavigation() } }
    }
}

@Composable
fun AppNavigation() {
    val navController = rememberNavController()

    NavHost(navController = navController, startDestination = "home") {
        composable("home") {
            Column(
                modifier = Modifier.fillMaxSize().padding(32.dp),
                horizontalAlignment = Alignment.CenterHorizontally,
                verticalArrangement = Arrangement.Center
            ) {
                Text("Home Screen", fontSize = 28.sp, fontWeight = FontWeight.Bold)
                Spacer(modifier = Modifier.height(16.dp))
                Button(onClick = { navController.navigate("detail/42") }) {
                    Text("Go to Detail #42")
                }
                Spacer(modifier = Modifier.height(8.dp))
                Button(onClick = { navController.navigate("settings") }) {
                    Text("Go to Settings")
                }
            }
        }

        composable("detail/{itemId}") { backStackEntry ->
            val itemId = backStackEntry.arguments?.getString("itemId") ?: "0"
            Column(
                modifier = Modifier.fillMaxSize().padding(32.dp),
                horizontalAlignment = Alignment.CenterHorizontally,
                verticalArrangement = Arrangement.Center
            ) {
                Text("Detail Screen", fontSize = 28.sp, fontWeight = FontWeight.Bold)
                Text("Item ID: $itemId", fontSize = 22.sp)
                Spacer(modifier = Modifier.height(16.dp))
                Button(onClick = { navController.popBackStack() }) {
                    Text("Go Back")
                }
            }
        }

        composable("settings") {
            Column(
                modifier = Modifier.fillMaxSize().padding(32.dp),
                horizontalAlignment = Alignment.CenterHorizontally,
                verticalArrangement = Arrangement.Center
            ) {
                Text("Settings Screen", fontSize = 28.sp, fontWeight = FontWeight.Bold)
                Spacer(modifier = Modifier.height(16.dp))
                Button(onClick = { navController.popBackStack() }) {
                    Text("Go Back")
                }
            }
        }
    }
}
```

---

## Gradle Dependencies Reference

Add these to your `build.gradle (Module)`:

```gradle
dependencies {
    // Compose BOM (manages all Compose versions)
    implementation platform('androidx.compose:compose-bom:2024.02.00')
    implementation 'androidx.compose.ui:ui'
    implementation 'androidx.compose.material3:material3'
    implementation 'androidx.compose.ui:ui-tooling-preview'

    // Navigation
    implementation 'androidx.navigation:navigation-compose:2.7.7'

    // DataStore
    implementation 'androidx.datastore:datastore-preferences:1.1.1'

    // Foundation (Pager)
    implementation 'androidx.compose.foundation:foundation'

    // Icons
    implementation 'androidx.compose.material:material-icons-extended'

    // Activity Compose
    implementation 'androidx.activity:activity-compose:1.8.2'
}
```

---
