# Unit 6: Advanced Navigation & Paging UI Components in Jetpack Compose

---

## Key Definitions (Must Know for Viva)

| Keyword | Definition |
|---|---|
| **TabRow** | A Material3 composable that displays a horizontal row of tabs. Each tab represents a section/page. Users can tap a tab to switch content. |
| **ScrollableTabRow** | A variation of TabRow that scrolls horizontally when there are too many tabs to fit on screen. |
| **Tab** | An individual tab item inside a TabRow. Has `selected`, `onClick`, `text`, and `icon` parameters. |
| **HorizontalPager** | A composable that provides horizontal swipe navigation between pages (like ViewPager in XML). Each page is a full-screen composable. |
| **VerticalPager** | Similar to HorizontalPager but pages are swiped vertically (up/down) instead of horizontally. |
| **PagerState** | A state holder for HorizontalPager/VerticalPager that tracks the current page, page count, and provides functions to scroll to specific pages. |
| **rememberPagerState** | Creates and remembers a PagerState across recompositions. |
| **ModalNavigationDrawer** | A navigation drawer that slides in from the left side of the screen over the main content. It's modal — it dims the background and blocks interaction with main content. |
| **NavigationDrawer** | A permanent or dismissible navigation drawer. The permanent variant is always visible (typically on tablets). |
| **DrawerState** | A state holder for the navigation drawer that tracks whether it's open or closed. |
| **rememberDrawerState** | Creates and remembers a DrawerState across recompositions. |
| **DrawerValue.Closed / DrawerValue.Open** | The two possible states of a navigation drawer. |
| **NavigationDrawerItem** | A composable representing a single item in a navigation drawer (with icon, label, selected state). |
| **ModalDrawerSheet** | The container composable for the content inside a ModalNavigationDrawer. |
| **Navigation Component** | A Jetpack library for managing app navigation (screens, back stack, arguments). Uses `NavHost`, `NavController`, and `NavGraph`. |
| **NavHost** | A composable that hosts navigation content. It defines the navigation graph with routes and their corresponding composable screens. |
| **NavController** | The central controller for navigation. It manages the back stack and provides methods to navigate between screens (`navigate()`, `popBackStack()`). |
| **rememberNavController** | Creates and remembers a NavController across recompositions. |
| **Route** | A string identifier for a screen in the navigation graph. Example: `"home"`, `"profile/{userId}"`. |
| **Single Activity Architecture** | An app architecture where the entire app runs in a single Activity, and navigation between screens is handled by swapping composables (not Activities). Recommended for Compose apps. |
| **animateScrollToPage** | A suspend function on PagerState that animates scrolling to a specific page. |
| **currentPage** | A property of PagerState that returns the index of the currently visible page. |

---

## 6.1 TabRow + HorizontalPager

### Basic TabRow

```kotlin
@Composable
fun BasicTabRowExample() {
    var selectedTab by remember { mutableStateOf(0) }
    val tabs = listOf("Home", "Profile", "Settings")

    Column(modifier = Modifier.fillMaxSize()) {
        TabRow(selectedTabIndex = selectedTab) {
            tabs.forEachIndexed { index, title ->
                Tab(
                    selected = selectedTab == index,
                    onClick = { selectedTab = index },
                    text = { Text(title) },
                    icon = {
                        when (index) {
                            0 -> Icon(Icons.Default.Home, contentDescription = null)
                            1 -> Icon(Icons.Default.Person, contentDescription = null)
                            2 -> Icon(Icons.Default.Settings, contentDescription = null)
                        }
                    }
                )
            }
        }

        // Content based on selected tab
        when (selectedTab) {
            0 -> HomeContent()
            1 -> ProfileContent()
            2 -> SettingsContent()
        }
    }
}

@Composable
fun HomeContent() {
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Text("Home Screen", fontSize = 24.sp)
    }
}

@Composable
fun ProfileContent() {
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Text("Profile Screen", fontSize = 24.sp)
    }
}

@Composable
fun SettingsContent() {
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Text("Settings Screen", fontSize = 24.sp)
    }
}
```

### TabRow + HorizontalPager (Swipeable Tabs)

```kotlin
@OptIn(ExperimentalFoundationApi::class)
@Composable
fun TabPagerExample() {
    val tabs = listOf("Home", "Search", "Profile")
    val pagerState = rememberPagerState(pageCount = { tabs.size })
    val coroutineScope = rememberCoroutineScope()

    Column(modifier = Modifier.fillMaxSize()) {
        // Tab Row
        TabRow(selectedTabIndex = pagerState.currentPage) {
            tabs.forEachIndexed { index, title ->
                Tab(
                    selected = pagerState.currentPage == index,
                    onClick = {
                        // Animate scroll to the selected tab
                        coroutineScope.launch {
                            pagerState.animateScrollToPage(index)
                        }
                    },
                    text = { Text(title) }
                )
            }
        }

        // Horizontal Pager (swipeable content)
        HorizontalPager(
            state = pagerState,
            modifier = Modifier.fillMaxSize()
        ) { page ->
            Box(
                modifier = Modifier.fillMaxSize(),
                contentAlignment = Alignment.Center
            ) {
                Text(
                    text = "${tabs[page]} Screen",
                    fontSize = 28.sp,
                    fontWeight = FontWeight.Bold
                )
            }
        }
    }
}
```

### ScrollableTabRow (Many Tabs)

```kotlin
@OptIn(ExperimentalFoundationApi::class)
@Composable
fun ScrollableTabExample() {
    val tabs = listOf("Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")
    val pagerState = rememberPagerState(pageCount = { tabs.size })
    val scope = rememberCoroutineScope()

    Column {
        ScrollableTabRow(
            selectedTabIndex = pagerState.currentPage,
            edgePadding = 16.dp
        ) {
            tabs.forEachIndexed { index, title ->
                Tab(
                    selected = pagerState.currentPage == index,
                    onClick = {
                        scope.launch { pagerState.animateScrollToPage(index) }
                    },
                    text = { Text(title) }
                )
            }
        }

        HorizontalPager(state = pagerState) { page ->
            Box(
                modifier = Modifier.fillMaxSize(),
                contentAlignment = Alignment.Center
            ) {
                Text("Schedule for ${tabs[page]}", fontSize = 24.sp)
            }
        }
    }
}
```

**Viva Q: What is the difference between TabRow and ScrollableTabRow?**
> `TabRow` divides the available width equally among all tabs — suitable for 2-4 tabs. `ScrollableTabRow` allows horizontal scrolling when there are too many tabs to fit — each tab takes its natural width. Use ScrollableTabRow when you have 5+ tabs.

**Viva Q: How do you connect TabRow with HorizontalPager?**
> Use `rememberPagerState` to create shared state. Set `TabRow(selectedTabIndex = pagerState.currentPage)` and in each Tab's `onClick`, call `pagerState.animateScrollToPage(index)` using a coroutine scope. The pager automatically updates tabs when swiped, and tabs update the pager when clicked.

---

## 6.2 ModalNavigationDrawer

```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun NavigationDrawerExample() {
    val drawerState = rememberDrawerState(initialValue = DrawerValue.Closed)
    val scope = rememberCoroutineScope()
    var selectedItem by remember { mutableStateOf("Home") }

    val menuItems = listOf(
        "Home" to Icons.Default.Home,
        "Profile" to Icons.Default.Person,
        "Settings" to Icons.Default.Settings,
        "About" to Icons.Default.Info,
        "Logout" to Icons.Default.ExitToApp
    )

    ModalNavigationDrawer(
        drawerState = drawerState,
        drawerContent = {
            ModalDrawerSheet {
                // Header
                Box(
                    modifier = Modifier
                        .fillMaxWidth()
                        .height(150.dp)
                        .background(
                            Brush.verticalGradient(
                                listOf(Color(0xFF6200EE), Color(0xFF3700B3))
                            )
                        ),
                    contentAlignment = Alignment.BottomStart
                ) {
                    Column(modifier = Modifier.padding(16.dp)) {
                        Icon(
                            Icons.Default.AccountCircle,
                            contentDescription = null,
                            modifier = Modifier.size(48.dp),
                            tint = Color.White
                        )
                        Spacer(modifier = Modifier.height(8.dp))
                        Text("John Doe", color = Color.White, fontWeight = FontWeight.Bold)
                        Text("john@example.com", color = Color.White.copy(alpha = 0.7f))
                    }
                }

                Spacer(modifier = Modifier.height(8.dp))

                // Menu Items
                menuItems.forEach { (label, icon) ->
                    NavigationDrawerItem(
                        icon = { Icon(icon, contentDescription = null) },
                        label = { Text(label) },
                        selected = selectedItem == label,
                        onClick = {
                            selectedItem = label
                            scope.launch { drawerState.close() }
                        },
                        modifier = Modifier.padding(horizontal = 12.dp)
                    )
                }
            }
        }
    ) {
        // Main Content
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text(selectedItem) },
                    navigationIcon = {
                        IconButton(onClick = {
                            scope.launch { drawerState.open() }
                        }) {
                            Icon(Icons.Default.Menu, contentDescription = "Menu")
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
                Text("$selectedItem Screen", fontSize = 24.sp)
            }
        }
    }
}
```

**Viva Q: What is ModalNavigationDrawer?**
> ModalNavigationDrawer is a composable that creates a side navigation drawer that slides in from the left. It's "modal" because when open, it overlays the content and dims the background, blocking interaction with the main content. It contains `drawerContent` (the drawer UI) and the main content.

**Viva Q: How do you open/close a Navigation Drawer programmatically?**
> Use `drawerState.open()` and `drawerState.close()` — these are suspend functions, so call them inside a coroutine: `scope.launch { drawerState.open() }`. The `drawerState` is created using `rememberDrawerState(DrawerValue.Closed)`.

---

## 6.3 HorizontalPager / VerticalPager

### HorizontalPager (Image Carousel)

```kotlin
@OptIn(ExperimentalFoundationApi::class)
@Composable
fun ImageCarousel() {
    val images = listOf(Color.Red, Color.Blue, Color.Green, Color.Yellow, Color.Magenta)
    val pagerState = rememberPagerState(pageCount = { images.size })

    Column(
        modifier = Modifier.fillMaxSize(),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        // Pager
        HorizontalPager(
            state = pagerState,
            modifier = Modifier
                .fillMaxWidth()
                .height(300.dp)
        ) { page ->
            Card(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(16.dp),
                shape = RoundedCornerShape(16.dp)
            ) {
                Box(
                    modifier = Modifier
                        .fillMaxSize()
                        .background(images[page]),
                    contentAlignment = Alignment.Center
                ) {
                    Text(
                        "Page ${page + 1}",
                        color = Color.White,
                        fontSize = 32.sp,
                        fontWeight = FontWeight.Bold
                    )
                }
            }
        }

        Spacer(modifier = Modifier.height(16.dp))

        // Page Indicator (Dots)
        Row(
            horizontalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            repeat(images.size) { index ->
                Box(
                    modifier = Modifier
                        .size(if (pagerState.currentPage == index) 12.dp else 8.dp)
                        .clip(CircleShape)
                        .background(
                            if (pagerState.currentPage == index)
                                Color(0xFF6200EE)
                            else
                                Color.LightGray
                        )
                )
            }
        }

        Spacer(modifier = Modifier.height(8.dp))
        Text("Page ${pagerState.currentPage + 1} of ${images.size}")
    }
}
```

### VerticalPager

```kotlin
@OptIn(ExperimentalFoundationApi::class)
@Composable
fun VerticalPagerExample() {
    val pages = listOf("Welcome", "Features", "Get Started")
    val pagerState = rememberPagerState(pageCount = { pages.size })

    Box(modifier = Modifier.fillMaxSize()) {
        VerticalPager(
            state = pagerState,
            modifier = Modifier.fillMaxSize()
        ) { page ->
            Box(
                modifier = Modifier
                    .fillMaxSize()
                    .background(
                        when (page) {
                            0 -> Color(0xFF6200EE)
                            1 -> Color(0xFF03DAC5)
                            else -> Color(0xFFBB86FC)
                        }
                    ),
                contentAlignment = Alignment.Center
            ) {
                Column(horizontalAlignment = Alignment.CenterHorizontally) {
                    Text(
                        text = pages[page],
                        color = Color.White,
                        fontSize = 32.sp,
                        fontWeight = FontWeight.Bold
                    )
                    Spacer(modifier = Modifier.height(8.dp))
                    Text(
                        "Swipe up for next",
                        color = Color.White.copy(alpha = 0.7f)
                    )
                }
            }
        }

        // Side indicator
        Column(
            modifier = Modifier
                .align(Alignment.CenterEnd)
                .padding(end = 16.dp),
            verticalArrangement = Arrangement.spacedBy(8.dp)
        ) {
            repeat(pages.size) { index ->
                Box(
                    modifier = Modifier
                        .size(if (pagerState.currentPage == index) 12.dp else 8.dp)
                        .clip(CircleShape)
                        .background(
                            if (pagerState.currentPage == index) Color.White
                            else Color.White.copy(alpha = 0.5f)
                        )
                )
            }
        }
    }
}
```

**Viva Q: What is HorizontalPager?**
> HorizontalPager is a composable that allows users to swipe horizontally between full-screen pages. It's the Compose equivalent of ViewPager. It uses `PagerState` to track the current page. Each page is a composable function.

**Viva Q: What is the difference between HorizontalPager and VerticalPager?**
> HorizontalPager swipes left/right between pages. VerticalPager swipes up/down. Both use the same `PagerState` and have the same API. Use HorizontalPager for tab-like content, VerticalPager for onboarding or feed-style content.

---

## 6.4 Navigation with NavHost (Bonus)

```kotlin
@Composable
fun AppNavigation() {
    val navController = rememberNavController()

    NavHost(
        navController = navController,
        startDestination = "home"
    ) {
        composable("home") {
            HomeScreen(
                onNavigateToDetail = { id ->
                    navController.navigate("detail/$id")
                }
            )
        }
        composable("detail/{itemId}") { backStackEntry ->
            val itemId = backStackEntry.arguments?.getString("itemId") ?: "0"
            DetailScreen(
                itemId = itemId,
                onBack = { navController.popBackStack() }
            )
        }
    }
}

@Composable
fun HomeScreen(onNavigateToDetail: (String) -> Unit) {
    Column(
        modifier = Modifier.fillMaxSize().padding(16.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text("Home Screen", fontSize = 24.sp)
        Spacer(modifier = Modifier.height(16.dp))
        Button(onClick = { onNavigateToDetail("42") }) {
            Text("Go to Detail #42")
        }
    }
}

@Composable
fun DetailScreen(itemId: String, onBack: () -> Unit) {
    Column(
        modifier = Modifier.fillMaxSize().padding(16.dp),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text("Detail Screen — Item $itemId", fontSize = 24.sp)
        Spacer(modifier = Modifier.height(16.dp))
        Button(onClick = onBack) {
            Text("Go Back")
        }
    }
}
```

**Viva Q: What is NavHost?**
> NavHost is a composable that acts as a container for navigation. It defines the navigation graph — mapping route strings to composable screens. It uses a NavController to manage the back stack and handle navigation between screens.

**Viva Q: What is Single Activity Architecture?**
> It's an architecture where the entire app uses a single Activity, and navigation between screens is done by swapping composables using NavHost + NavController. Instead of starting new Activities, you navigate to different composable routes. This is the recommended approach for Jetpack Compose apps.

---

## Viva Questions & Answers

**Q1: What is a PagerState?**
> PagerState is a state holder for HorizontalPager/VerticalPager. It tracks the current page index (`currentPage`), page count, and provides functions to scroll programmatically (`animateScrollToPage()`, `scrollToPage()`).

**Q2: How do you create a page indicator (dots) for a Pager?**
> Use a Row of small circles (Box with CircleShape). Loop through page count, and for each index, check if it matches `pagerState.currentPage`. If it does, make it bigger/colored; otherwise, make it smaller/gray.

**Q3: What is the difference between ModalNavigationDrawer and permanent NavigationDrawer?**
> ModalNavigationDrawer slides over the content, dims the background, and blocks interaction (used on phones). Permanent NavigationDrawer is always visible alongside the content (used on tablets/large screens).

**Q4: How do you pass arguments in Navigation Compose?**
> Define the route with placeholders: `"detail/{itemId}"`. Navigate using `navController.navigate("detail/42")`. Access the argument in the destination: `backStackEntry.arguments?.getString("itemId")`.

**Q5: What is `animateScrollToPage`?**
> A suspend function on PagerState that smoothly animates the pager from the current page to the specified page. Must be called inside a coroutine: `scope.launch { pagerState.animateScrollToPage(2) }`.

**Q6: What is `DrawerState`?**
> DrawerState tracks whether a navigation drawer is open or closed. Created with `rememberDrawerState(DrawerValue.Closed)`. Use `drawerState.open()` and `drawerState.close()` (suspend functions) to control it.

**Q7: What is a NavigationDrawerItem?**
> A Material3 composable representing a single item in a navigation drawer. It has parameters for `icon`, `label`, `selected` (boolean), and `onClick`. The selected item is visually highlighted.

**Q8: When would you use VerticalPager?**
> Use VerticalPager for onboarding screens (swipe up to continue), feed-style content (like TikTok/Instagram Reels), or any vertical page-by-page navigation.

---
