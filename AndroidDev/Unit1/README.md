# Unit 1: Views & Components in Jetpack Compose

---

## Key Definitions (Must Know for Viva)

| Keyword | Definition |
|---|---|
| **Jetpack Compose** | A modern, fully declarative UI toolkit for Android that uses Kotlin to build native UIs. Instead of XML layouts, you write composable functions. |
| **Composable** | A function annotated with `@Composable` that describes a piece of UI. It can call other composable functions. Composables are the building blocks of Jetpack Compose. |
| **Recomposition** | The process by which Compose re-executes composable functions when state changes, updating only the parts of the UI that changed. |
| **State** | A value that can change over time. When state changes, Compose automatically recomposes (re-draws) the UI that reads that state. |
| **remember** | A composable function that stores a single object in memory during composition and returns the same object during recomposition. It survives recomposition but NOT configuration changes. |
| **mutableStateOf** | Creates an observable state holder. When its value changes, Compose schedules recomposition for any composable reading it. |
| **LazyColumn** | A vertically scrolling list that only composes and lays out items that are currently visible on screen (similar to RecyclerView). |
| **LazyRow** | A horizontally scrolling list that only composes visible items. |
| **LazyVerticalGrid** | A grid layout that lazily composes items in a vertical grid format. |
| **Modifier** | An ordered, immutable collection of elements that decorate or add behavior to Compose UI elements (padding, size, click, background, etc.). |
| **Scaffold** | A layout composable that provides slots for common Material Design layout elements like TopAppBar, BottomBar, FloatingActionButton, and Drawer. |
| **LaunchedEffect** | A composable that runs a suspend function (coroutine) when it enters the composition. Used for one-time side effects like splash screen delays. |
| **Side Effect** | Any work that happens outside the scope of a composable function, like launching a coroutine, logging, or navigation. |
| **Column** | A layout composable that places its children vertically (one below another). |
| **Row** | A layout composable that places its children horizontally (side by side). |
| **Box** | A layout composable that stacks its children on top of each other (like FrameLayout). |
| **Spinner** | A dropdown menu that lets the user select one value from a list. In Compose, it is implemented using `DropdownMenu` and `DropdownMenuItem`. |
| **ProgressBar** | A UI element that shows progress of an operation. Can be linear (`LinearProgressIndicator`) or circular (`CircularProgressIndicator`). |
| **Splash Screen** | The first screen shown when an app launches, usually displaying a logo or animation before navigating to the main screen. |
| **TopAppBar** | A Material Design top app bar composable that displays a title, navigation icon, and action items. |
| **DropdownMenu** | A composable that displays a popup menu with a list of items when triggered. |
| **rememberCoroutineScope** | Returns a `CoroutineScope` bound to the composition. Allows launching coroutines from callbacks (like button clicks). |
| **Canvas** | A composable that allows custom drawing using the `DrawScope` API (draw circles, lines, rectangles, arcs, etc.). |
| **verticalScroll** | A Modifier that makes a Column scrollable vertically. Unlike LazyColumn, it composes all items at once. |
| **horizontalScroll** | A Modifier that makes a Row scrollable horizontally. |
| **nestedScroll** | A modifier that enables nested scroll behavior — allowing a parent and child to coordinate scrolling. |
| **items()** | A function used inside LazyColumn/LazyRow to define a list of items to display. |
| **rememberScrollState** | Creates and remembers a `ScrollState` for scrollable composables. |

---

## 1.1 Lists and Grids

### LazyColumn (Vertical List)

```kotlin
@Composable
fun StudentList() {
    val students = listOf("Amit", "Priya", "Rahul", "Sneha", "Vijay")

    LazyColumn(
        modifier = Modifier.fillMaxSize(),
        contentPadding = PaddingValues(16.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        items(students) { student ->
            Card(
                modifier = Modifier.fillMaxWidth(),
                elevation = CardDefaults.cardElevation(4.dp)
            ) {
                Text(
                    text = student,
                    modifier = Modifier.padding(16.dp),
                    fontSize = 18.sp
                )
            }
        }
    }
}
```

### LazyRow (Horizontal List)

```kotlin
@Composable
fun HorizontalImageList() {
    val colors = listOf(Color.Red, Color.Blue, Color.Green, Color.Yellow)

    LazyRow(
        contentPadding = PaddingValues(16.dp),
        horizontalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        items(colors) { color ->
            Box(
                modifier = Modifier
                    .size(100.dp)
                    .background(color, RoundedCornerShape(12.dp))
            )
        }
    }
}
```

### LazyVerticalGrid

```kotlin
@Composable
fun PhotoGrid() {
    val items = (1..20).toList()

    LazyVerticalGrid(
        columns = GridCells.Fixed(3),  // 3 columns
        contentPadding = PaddingValues(8.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp),
        horizontalArrangement = Arrangement.spacedBy(8.dp)
    ) {
        items(items) { item ->
            Card(
                modifier = Modifier
                    .fillMaxWidth()
                    .aspectRatio(1f),
                colors = CardDefaults.cardColors(
                    containerColor = Color(0xFF6200EE)
                )
            ) {
                Box(contentAlignment = Alignment.Center) {
                    Text("Item $item", color = Color.White)
                }
            }
        }
    }
}
```

**Viva Q: What is the difference between LazyColumn and Column with verticalScroll?**
> LazyColumn only composes items currently visible on screen (lazy loading), making it efficient for large lists. Column with `verticalScroll` composes ALL items at once, which can be slow for large data sets. LazyColumn is like RecyclerView; Column with scroll is like ScrollView.

---

## 1.2 Scroll and Nested Scroll

### Vertical Scroll

```kotlin
@Composable
fun ScrollableContent() {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .verticalScroll(rememberScrollState())
            .padding(16.dp)
    ) {
        repeat(50) { index ->
            Text(
                text = "Item #$index",
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(vertical = 8.dp),
                fontSize = 18.sp
            )
        }
    }
}
```

### Nested Scroll Example

```kotlin
@Composable
fun NestedScrollExample() {
    val outerScrollState = rememberScrollState()

    Column(
        modifier = Modifier
            .fillMaxSize()
            .verticalScroll(outerScrollState)
            .padding(16.dp)
    ) {
        Text("Header Section", fontSize = 24.sp, fontWeight = FontWeight.Bold)

        Spacer(modifier = Modifier.height(16.dp))

        // Inner horizontal scroll
        LazyRow(
            horizontalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            items(10) { index ->
                Card(
                    modifier = Modifier.size(120.dp)
                ) {
                    Box(contentAlignment = Alignment.Center) {
                        Text("Card $index")
                    }
                }
            }
        }

        Spacer(modifier = Modifier.height(16.dp))

        // More content below
        repeat(20) { index ->
            Text("Body Item $index", modifier = Modifier.padding(8.dp))
        }
    }
}
```

**Viva Q: What is Nested Scroll?**
> Nested Scroll is when a scrollable composable is placed inside another scrollable composable. The `nestedScroll` modifier allows parent and child to coordinate scrolling — for example, a horizontal LazyRow inside a vertical scrollable Column.

---

## 1.3 Adding Spinner to App

### Spinner (Dropdown) in Compose

```kotlin
@Composable
fun SpinnerExample() {
    var expanded by remember { mutableStateOf(false) }
    var selectedItem by remember { mutableStateOf("Select City") }
    val cities = listOf("Delhi", "Mumbai", "Bangalore", "Chennai", "Kolkata")

    Column(modifier = Modifier.padding(16.dp)) {

        // Dropdown Trigger Button
        OutlinedButton(onClick = { expanded = true }) {
            Text(text = selectedItem)
            Icon(Icons.Default.ArrowDropDown, contentDescription = null)
        }

        // Dropdown Menu
        DropdownMenu(
            expanded = expanded,
            onDismissRequest = { expanded = false }
        ) {
            cities.forEach { city ->
                DropdownMenuItem(
                    text = { Text(city) },
                    onClick = {
                        selectedItem = city
                        expanded = false
                    }
                )
            }
        }

        Spacer(modifier = Modifier.height(16.dp))
        Text("Selected: $selectedItem", fontSize = 18.sp)
    }
}
```

**Viva Q: How do you implement a Spinner in Jetpack Compose?**
> In Compose there is no direct Spinner widget. We use `DropdownMenu` with `DropdownMenuItem` composables. A button triggers `expanded = true`, and selecting an item sets the selection and closes the menu.

---

## 1.4 Splash Screen using LaunchedEffect

### What is LaunchedEffect?
`LaunchedEffect` runs a suspend function when it enters the composition. It takes a **key** parameter — the effect re-launches only when the key changes.

```kotlin
@Composable
fun SplashScreen(onNavigateToHome: () -> Unit) {
    // LaunchedEffect runs once when the composable enters composition
    LaunchedEffect(key1 = true) {
        delay(3000L)  // Wait 3 seconds
        onNavigateToHome()  // Navigate to Home screen
    }

    // Splash UI
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
            // App icon or logo
            Icon(
                imageVector = Icons.Default.Star,
                contentDescription = "Logo",
                tint = Color.White,
                modifier = Modifier.size(100.dp)
            )
            Spacer(modifier = Modifier.height(16.dp))
            Text(
                text = "My App",
                color = Color.White,
                fontSize = 32.sp,
                fontWeight = FontWeight.Bold
            )
            Spacer(modifier = Modifier.height(24.dp))
            CircularProgressIndicator(color = Color.White)
        }
    }
}
```

**Viva Q: What is LaunchedEffect and when do you use it?**
> `LaunchedEffect` is a side-effect API that launches a coroutine when the composable enters the composition. It is used for one-time operations like delays (splash screen), API calls, or animations. The `key1` parameter controls when the effect re-launches — if the key changes, the previous coroutine is cancelled and a new one starts.

**Viva Q: What is a side effect in Compose?**
> A side effect is work that escapes the scope of a composable function — like making a network call, writing to a database, or navigating to another screen. Compose provides APIs like `LaunchedEffect`, `SideEffect`, and `DisposableEffect` to handle side effects safely.

---

## 1.5 Progress Bar

### Linear Progress Bar

```kotlin
@Composable
fun LinearProgressExample() {
    var progress by remember { mutableStateOf(0f) }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("Download Progress: ${(progress * 100).toInt()}%")

        Spacer(modifier = Modifier.height(16.dp))

        // Determinate progress bar
        LinearProgressIndicator(
            progress = progress,
            modifier = Modifier
                .fillMaxWidth()
                .height(8.dp),
            color = Color(0xFF6200EE),
            trackColor = Color.LightGray
        )

        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = {
            if (progress < 1f) progress += 0.1f
        }) {
            Text("Increase Progress")
        }

        Spacer(modifier = Modifier.height(32.dp))

        // Indeterminate progress bar (no specific progress value)
        Text("Loading...")
        CircularProgressIndicator(color = Color(0xFF6200EE))
    }
}
```

### Circular Progress Bar

```kotlin
@Composable
fun CircularProgressExample() {
    var loading by remember { mutableStateOf(false) }

    Column(
        modifier = Modifier.fillMaxSize(),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        if (loading) {
            CircularProgressIndicator(
                modifier = Modifier.size(64.dp),
                color = Color(0xFF6200EE),
                strokeWidth = 6.dp
            )
        }

        Spacer(modifier = Modifier.height(16.dp))

        Button(onClick = { loading = !loading }) {
            Text(if (loading) "Stop" else "Start Loading")
        }
    }
}
```

**Viva Q: What is the difference between determinate and indeterminate progress bar?**
> **Determinate** shows specific progress (e.g., 50% downloaded) — you pass a `progress` value (0f to 1f). **Indeterminate** shows ongoing activity without a specific percentage — you don't pass a `progress` value, and it shows a continuous animation.

**Viva Q: How would you implement a progress bar in Compose?**
> Use `LinearProgressIndicator` for a horizontal bar or `CircularProgressIndicator` for a circular spinner. For determinate, pass `progress = floatValue`. For indeterminate, call the composable without a progress parameter.

---

## 1.6 Custom Rating Bar

```kotlin
@Composable
fun CustomRatingBar(
    maxStars: Int = 5,
    rating: Int,
    onRatingChanged: (Int) -> Unit
) {
    Row {
        for (i in 1..maxStars) {
            Icon(
                imageVector = if (i <= rating) Icons.Filled.Star
                              else Icons.Outlined.Star,
                contentDescription = "Star $i",
                tint = if (i <= rating) Color(0xFFFFD700) else Color.Gray,
                modifier = Modifier
                    .size(40.dp)
                    .clickable { onRatingChanged(i) }
            )
        }
    }
}

// Usage
@Composable
fun RatingBarScreen() {
    var rating by remember { mutableStateOf(0) }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(32.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text("Rate this app:", fontSize = 20.sp)

        Spacer(modifier = Modifier.height(16.dp))

        CustomRatingBar(
            maxStars = 5,
            rating = rating,
            onRatingChanged = { rating = it }
        )

        Spacer(modifier = Modifier.height(16.dp))

        Text("You rated: $rating / 5 stars", fontSize = 16.sp)
    }
}
```

**Viva Q: How would you implement a custom rating bar in Compose?**
> Create a Row of clickable Star icons. Use a loop from 1 to maxStars. If `i <= rating`, show a filled star (golden color); otherwise, show an outlined star (gray). On click, update the rating state. The state variable `rating` controls which stars are filled.

---

## 1.7 Menu (TopAppBar with Options Menu)

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MenuExample() {
    var expanded by remember { mutableStateOf(false) }
    var selectedItem by remember { mutableStateOf("Home") }

    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("My App") },
                actions = {
                    IconButton(onClick = { expanded = true }) {
                        Icon(Icons.Default.MoreVert, contentDescription = "Menu")
                    }
                    DropdownMenu(
                        expanded = expanded,
                        onDismissRequest = { expanded = false }
                    ) {
                        DropdownMenuItem(
                            text = { Text("Settings") },
                            onClick = {
                                selectedItem = "Settings"
                                expanded = false
                            }
                        )
                        DropdownMenuItem(
                            text = { Text("About") },
                            onClick = {
                                selectedItem = "About"
                                expanded = false
                            }
                        )
                        DropdownMenuItem(
                            text = { Text("Logout") },
                            onClick = {
                                selectedItem = "Logout"
                                expanded = false
                            }
                        )
                    }
                }
            )
        }
    ) { paddingValues ->
        Box(
            modifier = Modifier
                .fillMaxSize()
                .padding(paddingValues),
            contentAlignment = Alignment.Center
        ) {
            Text("Selected: $selectedItem", fontSize = 24.sp)
        }
    }
}
```

**Viva Q: How do you create an overflow menu (three-dot menu) in Compose?**
> Use `TopAppBar` with an `actions` slot. Inside actions, place an `IconButton` with `Icons.Default.MoreVert`. On click, set `expanded = true` to open a `DropdownMenu` containing `DropdownMenuItem` composables.

---

## Viva Questions & Answers

**Q1: What is Jetpack Compose?**
> Jetpack Compose is Android's modern, fully declarative UI toolkit. Instead of writing XML layouts and using `findViewById`, you write `@Composable` functions in Kotlin that describe your UI. The framework handles rendering and updates automatically when state changes.

**Q2: What is the difference between `remember` and `mutableStateOf`?**
> `mutableStateOf` creates an **observable state** — Compose watches it for changes. `remember` **stores** a value across recompositions. They are used together: `var x by remember { mutableStateOf(0) }`. Without `remember`, the state resets on every recomposition. Without `mutableStateOf`, Compose won't know the value changed.

**Q3: What is Recomposition?**
> Recomposition is the process of re-executing composable functions when their input state changes. Compose intelligently updates only the composables that read the changed state, not the entire UI tree. This makes Compose efficient.

**Q4: What are the three basic layout composables in Compose?**
> **Column** (places children vertically), **Row** (places children horizontally), and **Box** (stacks children on top of each other). These replace LinearLayout (vertical/horizontal) and FrameLayout from XML.

**Q5: What is a Modifier?**
> A Modifier is an ordered, immutable collection of elements that decorates or adds behavior to a composable. Examples: `Modifier.padding(16.dp)`, `.fillMaxSize()`, `.clickable { }`, `.background(Color.Red)`. Modifiers are chained and applied in order.

**Q6: What is Scaffold?**
> Scaffold is a Material Design layout composable that provides predefined slots for common layout elements — `topBar`, `bottomBar`, `floatingActionButton`, `drawerContent`, and `content`. It helps structure an app's main screen layout.

**Q7: What is the difference between LazyColumn and RecyclerView?**
> LazyColumn is the Compose equivalent of RecyclerView. Both lazily load items. But LazyColumn doesn't need an Adapter, ViewHolder, or LayoutManager — you just define items inside the `LazyColumn` block. It's much simpler.

**Q8: What is `rememberCoroutineScope`?**
> It returns a CoroutineScope tied to the composable's lifecycle. You use it to launch coroutines from event callbacks (like button clicks). Unlike `LaunchedEffect`, it doesn't launch automatically — you call `scope.launch { }` manually.

**Q9: How does state hoisting work?**
> State hoisting moves the state UP to a parent composable and passes the state VALUE and an onChange CALLBACK down to the child. This makes the child composable stateless and reusable. Example: the rating bar takes `rating` and `onRatingChanged` as parameters.

**Q10: What is `GridCells.Fixed(n)` vs `GridCells.Adaptive(minSize)`?**
> `Fixed(n)` creates exactly n columns. `Adaptive(minSize)` creates as many columns as can fit, with each being at least `minSize` wide. Adaptive is better for responsive layouts.

---
