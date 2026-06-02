# Unit 4: Custom UI Components in Jetpack Compose

---

## Key Definitions (Must Know for Viva)

| Keyword | Definition |
|---|---|
| **Material Design** | A design system created by Google that provides guidelines, components, and tools for building consistent, beautiful, and usable apps. Material 3 (Material You) is the latest version. |
| **Foundation Composables** | Basic building blocks in Compose that are not styled with Material design. Examples: `BasicTextField`, `BasicText`, `Canvas`, `Image`. They offer maximum customization. |
| **Material Composables** | Pre-styled components following Material Design guidelines. Examples: `Button`, `Text`, `TextField`, `Card`, `Checkbox`, `Switch`. They have built-in theming. |
| **Declarative UI** | A programming paradigm where you describe WHAT the UI should look like, not HOW to build it step by step. Compose re-renders automatically when state changes. |
| **Imperative UI** | Traditional Android approach (XML + View system) where you manually create views, find them by ID, and update them step by step. |
| **Modifier** | An ordered, immutable collection of elements that decorate or add behavior to composables. Applied using dot-chaining: `Modifier.padding().size().background()`. Order matters! |
| **Shape** | Defines the outline/border shape of a composable. Common shapes: `RoundedCornerShape`, `CircleShape`, `CutCornerShape`, `RectangleShape`. |
| **Color** | Represents a color in Compose. Can be created from hex (`Color(0xFF6200EE)`), named constants (`Color.Red`), or Material theme (`MaterialTheme.colorScheme.primary`). |
| **MaterialTheme** | A composable that defines the color scheme, typography, and shapes used throughout the app. Child composables access theme values via `MaterialTheme.colorScheme`, `MaterialTheme.typography`. |
| **Typography** | Defines text styles used in the app. Material3 provides styles like `displayLarge`, `headlineMedium`, `bodyLarge`, `labelSmall`, etc. |
| **ColorScheme** | A set of colors used by Material3 components. Includes `primary`, `secondary`, `tertiary`, `background`, `surface`, `error`, and their variants. |
| **@Composable** | An annotation that marks a function as a composable function — one that can emit UI elements and participate in Compose's composition system. |
| **Parameters** | Input values passed to a composable function that control its appearance and behavior (like text content, color, size, click handler). |
| **Slot API** | A pattern where a composable accepts other composables as parameters (using lambda `@Composable () -> Unit`), allowing flexible content injection. |
| **RoundedCornerShape** | A shape with rounded corners. `RoundedCornerShape(16.dp)` creates a shape with 16dp corner radius. |
| **CircleShape** | A perfectly circular shape, equivalent to `RoundedCornerShape(50%)`. |
| **CutCornerShape** | A shape with cut (diagonal) corners instead of rounded ones. |
| **clip** | A Modifier that clips the composable's content to a specific shape. |
| **border** | A Modifier that draws a border around the composable with specified width, color, and shape. |
| **shadow** | A Modifier that draws a shadow behind the composable with specified elevation and shape. |
| **BasicTextField** | A Foundation-level text input composable without Material styling. Allows full customization of appearance. |
| **OutlinedTextField** | A Material3 text field with an outlined border. Has built-in label, placeholder, and error support. |
| **TextStyle** | Defines the visual style of text — font size, font weight, color, letter spacing, line height, font family, etc. |

---

## 4.1 Material vs Foundation Composables

### Comparison:

| Feature | Material Composables | Foundation Composables |
|---|---|---|
| **Styling** | Pre-styled with Material Design | No default styling |
| **Theming** | Follows MaterialTheme | No theme awareness |
| **Customization** | Limited to Material design system | Maximum flexibility |
| **Examples** | `Button`, `Text`, `TextField`, `Card` | `BasicTextField`, `BasicText`, `Canvas` |
| **Use Case** | Standard UI following Material guidelines | Fully custom UI designs |

### Material Composables Examples:

```kotlin
// Material Button
Button(
    onClick = { /* action */ },
    colors = ButtonDefaults.buttonColors(
        containerColor = Color(0xFF6200EE)
    )
) {
    Text("Material Button")
}

// Material Card
Card(
    modifier = Modifier.fillMaxWidth(),
    elevation = CardDefaults.cardElevation(8.dp),
    shape = RoundedCornerShape(16.dp)
) {
    Text("Inside a Card", modifier = Modifier.padding(16.dp))
}
```

### Foundation Composables Examples:

```kotlin
// BasicTextField (no Material styling)
var text by remember { mutableStateOf("") }
BasicTextField(
    value = text,
    onValueChange = { text = it },
    modifier = Modifier
        .fillMaxWidth()
        .background(Color.LightGray, RoundedCornerShape(8.dp))
        .padding(16.dp),
    textStyle = TextStyle(fontSize = 18.sp, color = Color.Black)
)
```

**Viva Q: What is the difference between Material and Foundation composables?**
> Material composables (`Button`, `TextField`, `Card`) come pre-styled with Material Design guidelines and follow the app's theme. Foundation composables (`BasicTextField`, `Canvas`) have no default styling, giving complete control over appearance. Use Material for standard apps, Foundation for fully custom designs.

---

## 4.2 Fully Declarative UI Approach

### Declarative vs Imperative:

**Imperative (Old XML Way):**
```kotlin
// Find view, then update it manually
val textView = findViewById<TextView>(R.id.myText)
textView.text = "Hello"
textView.setTextColor(Color.RED)
textView.visibility = View.VISIBLE
```

**Declarative (Compose Way):**
```kotlin
// Describe WHAT the UI should look like
@Composable
fun Greeting(name: String, isVisible: Boolean) {
    if (isVisible) {
        Text(
            text = "Hello, $name!",
            color = Color.Red,
            fontSize = 20.sp
        )
    }
}
```

**Viva Q: What does "fully declarative" mean in Jetpack Compose?**
> In a declarative approach, you describe WHAT the UI should look like based on the current state, and the framework handles HOW to update it. You don't manually find views or update them. When state changes, Compose automatically re-executes (recomposes) the relevant composable functions and updates the UI.

---

## 4.3 Creating Custom Text

```kotlin
@Composable
fun CustomText(
    text: String,
    modifier: Modifier = Modifier,
    fontSize: TextUnit = 16.sp,
    fontWeight: FontWeight = FontWeight.Normal,
    color: Color = Color.Black,
    textAlign: TextAlign = TextAlign.Start,
    maxLines: Int = Int.MAX_VALUE,
    fontFamily: FontFamily = FontFamily.Default
) {
    Text(
        text = text,
        modifier = modifier,
        fontSize = fontSize,
        fontWeight = fontWeight,
        color = color,
        textAlign = textAlign,
        maxLines = maxLines,
        overflow = TextOverflow.Ellipsis,
        fontFamily = fontFamily,
        style = TextStyle(
            letterSpacing = 0.5.sp,
            lineHeight = 24.sp
        )
    )
}

// Usage
@Composable
fun TextExamples() {
    Column(modifier = Modifier.padding(16.dp)) {
        // Title text
        CustomText(
            text = "Welcome to My App",
            fontSize = 28.sp,
            fontWeight = FontWeight.Bold,
            color = Color(0xFF6200EE)
        )

        Spacer(modifier = Modifier.height(8.dp))

        // Body text
        CustomText(
            text = "This is body text with custom styling",
            fontSize = 16.sp,
            color = Color.Gray
        )

        Spacer(modifier = Modifier.height(8.dp))

        // Text with gradient (advanced)
        Text(
            text = "Gradient Text",
            fontSize = 32.sp,
            fontWeight = FontWeight.Bold,
            style = TextStyle(
                brush = Brush.linearGradient(
                    colors = listOf(Color(0xFF6200EE), Color(0xFFBB86FC))
                )
            )
        )
    }
}
```

---

## 4.4 Creating Custom TextField

```kotlin
@Composable
fun CustomTextField(
    value: String,
    onValueChange: (String) -> Unit,
    label: String,
    modifier: Modifier = Modifier,
    leadingIcon: ImageVector? = null,
    isPassword: Boolean = false,
    isError: Boolean = false,
    errorMessage: String = ""
) {
    Column {
        OutlinedTextField(
            value = value,
            onValueChange = onValueChange,
            label = { Text(label) },
            modifier = modifier.fillMaxWidth(),
            leadingIcon = leadingIcon?.let {
                { Icon(it, contentDescription = null) }
            },
            visualTransformation = if (isPassword)
                PasswordVisualTransformation()
            else
                VisualTransformation.None,
            isError = isError,
            shape = RoundedCornerShape(12.dp),
            colors = OutlinedTextFieldDefaults.colors(
                focusedBorderColor = Color(0xFF6200EE),
                unfocusedBorderColor = Color.Gray,
                errorBorderColor = Color.Red,
                focusedLabelColor = Color(0xFF6200EE)
            ),
            singleLine = true
        )

        if (isError && errorMessage.isNotEmpty()) {
            Text(
                text = errorMessage,
                color = Color.Red,
                fontSize = 12.sp,
                modifier = Modifier.padding(start = 8.dp, top = 4.dp)
            )
        }
    }
}

// Usage
@Composable
fun LoginForm() {
    var email by remember { mutableStateOf("") }
    var password by remember { mutableStateOf("") }

    Column(modifier = Modifier.padding(24.dp)) {
        CustomTextField(
            value = email,
            onValueChange = { email = it },
            label = "Email",
            leadingIcon = Icons.Default.Email
        )

        Spacer(modifier = Modifier.height(16.dp))

        CustomTextField(
            value = password,
            onValueChange = { password = it },
            label = "Password",
            leadingIcon = Icons.Default.Lock,
            isPassword = true
        )
    }
}
```

### Fully Custom TextField using BasicTextField

```kotlin
@Composable
fun FullyCustomTextField(
    value: String,
    onValueChange: (String) -> Unit,
    placeholder: String = "Type here..."
) {
    BasicTextField(
        value = value,
        onValueChange = onValueChange,
        modifier = Modifier
            .fillMaxWidth()
            .background(Color(0xFFF5F5F5), RoundedCornerShape(12.dp))
            .padding(horizontal = 16.dp, vertical = 14.dp),
        textStyle = TextStyle(
            fontSize = 16.sp,
            color = Color.Black
        ),
        decorationBox = { innerTextField ->
            Box {
                if (value.isEmpty()) {
                    Text(
                        text = placeholder,
                        color = Color.Gray,
                        fontSize = 16.sp
                    )
                }
                innerTextField()  // The actual text field
            }
        }
    )
}
```

**Viva Q: What is the difference between TextField, OutlinedTextField, and BasicTextField?**
> `TextField` — Material3 filled text field with background color. `OutlinedTextField` — Material3 text field with an outline border. `BasicTextField` — Foundation composable with NO styling at all; you build the entire UI yourself using `decorationBox`. Use BasicTextField for fully custom designs.

---

## 4.5 Creating Custom Button

```kotlin
@Composable
fun CustomButton(
    text: String,
    onClick: () -> Unit,
    modifier: Modifier = Modifier,
    backgroundColor: Color = Color(0xFF6200EE),
    textColor: Color = Color.White,
    shape: Shape = RoundedCornerShape(12.dp),
    enabled: Boolean = true,
    icon: ImageVector? = null
) {
    Button(
        onClick = onClick,
        modifier = modifier.height(50.dp),
        enabled = enabled,
        shape = shape,
        colors = ButtonDefaults.buttonColors(
            containerColor = backgroundColor,
            contentColor = textColor,
            disabledContainerColor = Color.Gray,
            disabledContentColor = Color.White
        ),
        elevation = ButtonDefaults.buttonElevation(
            defaultElevation = 6.dp,
            pressedElevation = 2.dp
        )
    ) {
        if (icon != null) {
            Icon(icon, contentDescription = null, modifier = Modifier.size(20.dp))
            Spacer(modifier = Modifier.width(8.dp))
        }
        Text(text = text, fontSize = 16.sp, fontWeight = FontWeight.Bold)
    }
}

// Usage
@Composable
fun ButtonExamples() {
    Column(
        modifier = Modifier.fillMaxSize().padding(24.dp),
        verticalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        // Primary Button
        CustomButton(
            text = "Primary Button",
            onClick = { },
            modifier = Modifier.fillMaxWidth()
        )

        // Button with Icon
        CustomButton(
            text = "Add to Cart",
            onClick = { },
            icon = Icons.Default.ShoppingCart,
            backgroundColor = Color(0xFF4CAF50),
            modifier = Modifier.fillMaxWidth()
        )

        // Outlined Button
        OutlinedButton(
            onClick = { },
            modifier = Modifier.fillMaxWidth().height(50.dp),
            shape = RoundedCornerShape(12.dp),
            border = BorderStroke(2.dp, Color(0xFF6200EE))
        ) {
            Text("Outlined Button", color = Color(0xFF6200EE))
        }

        // Text Button
        TextButton(onClick = { }) {
            Text("Text Button", color = Color(0xFF6200EE))
        }

        // Icon Button
        IconButton(onClick = { }) {
            Icon(
                Icons.Default.Favorite,
                contentDescription = "Like",
                tint = Color.Red
            )
        }
    }
}
```

---

## 4.6 Modifier Deep Dive

### Common Modifiers:

```kotlin
@Composable
fun ModifierShowcase() {
    Column(modifier = Modifier.padding(16.dp)) {

        // Size modifiers
        Box(modifier = Modifier
            .size(100.dp)               // fixed size
            .background(Color.Red)
        )

        Box(modifier = Modifier
            .fillMaxWidth()             // full width
            .height(50.dp)              // fixed height
            .background(Color.Blue)
        )

        // Padding (ORDER MATTERS!)
        Text(
            "Padding Demo",
            modifier = Modifier
                .background(Color.Yellow) // background first
                .padding(16.dp)           // then padding inside
        )

        // vs
        Text(
            "Padding Demo 2",
            modifier = Modifier
                .padding(16.dp)           // padding first (outside)
                .background(Color.Yellow) // then background
        )

        // Click + Ripple
        Box(
            modifier = Modifier
                .size(100.dp)
                .clip(RoundedCornerShape(16.dp))
                .background(Color(0xFF6200EE))
                .clickable { /* handle click */ }
                .padding(16.dp)
        )

        // Border
        Text(
            "Bordered Text",
            modifier = Modifier
                .border(2.dp, Color.Black, RoundedCornerShape(8.dp))
                .padding(12.dp)
        )

        // Shadow
        Card(
            modifier = Modifier
                .fillMaxWidth()
                .shadow(8.dp, RoundedCornerShape(16.dp))
        ) {
            Text("Card with Shadow", modifier = Modifier.padding(16.dp))
        }
    }
}
```

**Viva Q: Why does order matter in Modifiers?**
> Modifiers are applied **in order from top to bottom** (left to right in chaining). For example, `Modifier.background(Color.Red).padding(16.dp)` applies background first, THEN padding (padding is inside the background). But `Modifier.padding(16.dp).background(Color.Red)` applies padding first (creating space), THEN background (background doesn't cover the padding area). The order changes the visual result.

---

## 4.7 Shape

```kotlin
@Composable
fun ShapeExamples() {
    Column(
        modifier = Modifier.padding(16.dp),
        verticalArrangement = Arrangement.spacedBy(12.dp)
    ) {
        // Rounded Corner Shape
        Box(
            modifier = Modifier
                .size(100.dp)
                .clip(RoundedCornerShape(16.dp))
                .background(Color(0xFF6200EE))
        )

        // Circle Shape
        Box(
            modifier = Modifier
                .size(100.dp)
                .clip(CircleShape)
                .background(Color(0xFFE91E63))
        )

        // Cut Corner Shape
        Box(
            modifier = Modifier
                .size(100.dp)
                .clip(CutCornerShape(16.dp))
                .background(Color(0xFF4CAF50))
        )

        // Rectangle Shape (default)
        Box(
            modifier = Modifier
                .size(width = 150.dp, height = 80.dp)
                .clip(RectangleShape)
                .background(Color(0xFFFF9800))
        )

        // Different corners
        Box(
            modifier = Modifier
                .size(120.dp)
                .clip(RoundedCornerShape(
                    topStart = 32.dp,
                    topEnd = 0.dp,
                    bottomEnd = 32.dp,
                    bottomStart = 0.dp
                ))
                .background(Color(0xFF2196F3))
        )
    }
}
```

---

## 4.8 Color

```kotlin
@Composable
fun ColorExamples() {
    Column(modifier = Modifier.padding(16.dp)) {
        // From Hex
        Text("Hex Color", color = Color(0xFF6200EE))

        // Named Colors
        Text("Red", color = Color.Red)
        Text("Blue", color = Color.Blue)

        // RGBA
        Text("Custom RGBA", color = Color(red = 0.2f, green = 0.6f, blue = 1f, alpha = 1f))

        // From Material Theme
        Text(
            "Theme Primary",
            color = MaterialTheme.colorScheme.primary
        )

        // Gradient
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(60.dp)
                .background(
                    Brush.horizontalGradient(
                        listOf(Color(0xFF6200EE), Color(0xFFBB86FC))
                    )
                )
        )
    }
}
```

---

## 4.9 Custom Material Theme

```kotlin
// Define custom colors
private val DarkColorScheme = darkColorScheme(
    primary = Color(0xFFBB86FC),
    secondary = Color(0xFF03DAC5),
    tertiary = Color(0xFF3700B3),
    background = Color(0xFF121212),
    surface = Color(0xFF1E1E1E)
)

private val LightColorScheme = lightColorScheme(
    primary = Color(0xFF6200EE),
    secondary = Color(0xFF03DAC5),
    tertiary = Color(0xFF3700B3),
    background = Color(0xFFF5F5F5),
    surface = Color(0xFFFFFFFF)
)

// Define custom typography
private val AppTypography = Typography(
    headlineLarge = TextStyle(
        fontWeight = FontWeight.Bold,
        fontSize = 28.sp
    ),
    bodyLarge = TextStyle(
        fontSize = 16.sp,
        lineHeight = 24.sp
    )
)

// Define custom shapes
private val AppShapes = Shapes(
    small = RoundedCornerShape(4.dp),
    medium = RoundedCornerShape(12.dp),
    large = RoundedCornerShape(24.dp)
)

// Apply theme
@Composable
fun MyAppTheme(
    darkTheme: Boolean = isSystemInDarkTheme(),
    content: @Composable () -> Unit
) {
    val colorScheme = if (darkTheme) DarkColorScheme else LightColorScheme

    MaterialTheme(
        colorScheme = colorScheme,
        typography = AppTypography,
        shapes = AppShapes,
        content = content
    )
}

// Usage in Activity
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyAppTheme {
                Surface(color = MaterialTheme.colorScheme.background) {
                    // App content here
                    Text(
                        "Themed Text",
                        style = MaterialTheme.typography.headlineLarge,
                        color = MaterialTheme.colorScheme.primary
                    )
                }
            }
        }
    }
}
```

**Viva Q: What is MaterialTheme in Compose?**
> `MaterialTheme` is a composable that defines the color scheme, typography, and shapes for an app. All Material composables inside it automatically use the theme values. You access theme values with `MaterialTheme.colorScheme.primary`, `MaterialTheme.typography.bodyLarge`, etc.

---

## Viva Questions & Answers

**Q1: What is a Modifier in Jetpack Compose?**
> A Modifier is an ordered, immutable collection of elements that decorates or adds behavior to a composable — like padding, size, background, click handling, borders, and shapes. Modifiers are chained using dot notation and applied in order.

**Q2: What is the Slot API pattern?**
> The Slot API is a pattern where a composable function accepts other composable functions as parameters (lambdas of type `@Composable () -> Unit`). This allows flexible content injection. Example: `Scaffold` has slots for `topBar`, `content`, `floatingActionButton`.

**Q3: Name the three types of buttons in Material3 Compose.**
> `Button` (filled, primary action), `OutlinedButton` (bordered, secondary action), `TextButton` (text only, low emphasis). There's also `IconButton` and `FloatingActionButton`.

**Q4: What is `clip()` modifier?**
> `clip()` clips the content of a composable to a specified shape. For example, `Modifier.clip(CircleShape)` makes the content circular. It's often used with images and backgrounds.

**Q5: What is the difference between `dp` and `sp`?**
> `dp` (density-independent pixels) is used for layout dimensions — it scales with screen density. `sp` (scale-independent pixels) is used for font sizes — it scales with both screen density AND the user's font size preference.

**Q6: What is `decorationBox` in BasicTextField?**
> `decorationBox` is a parameter in `BasicTextField` that lets you wrap the actual text input with custom decorations — like placeholder text, icons, borders, or backgrounds. The `innerTextField()` call inside it renders the actual input field.

**Q7: How do you create a gradient background?**
> Use `Modifier.background(Brush.horizontalGradient(listOf(Color1, Color2)))` for horizontal gradient, or `Brush.verticalGradient()` for vertical, or `Brush.linearGradient()` for custom angle.

**Q8: What are Shapes in Compose?**
> Shapes define the outline of a composable. Common shapes: `RoundedCornerShape(radius)` (rounded corners), `CircleShape` (circle), `CutCornerShape(size)` (diagonal cut corners), `RectangleShape` (sharp corners).

---
