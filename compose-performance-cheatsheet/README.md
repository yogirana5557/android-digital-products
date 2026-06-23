# 🚀 Jetpack Compose Performance & Recomposition Cheat Sheet (Free Download)

Welcome to the open-source sample repository and reference checklist for the **Jetpack Compose Performance & Recomposition Cheat Sheet**.

This cheat sheet is a high-performance reference card detailing recomposition-bypass modifiers, state read deferrals, stability optimizations, stability report configurations, and lazy list recycling patterns.

---

## 🛍️ Get the PDF Edition (Free / $0+)

Get the print-ready, high-resolution 3-page PDF card to keep on your desktop or reference during development:
* [👉 **Download the PDF on Gumroad (Free / $0+)**](https://yogirana.gumroad.com/l/ftupd) *(Use this link to download the PDF, enter 0 to get it free!)*

---

## 📋 Cheat Sheet Reference Details

### 1. Deferring State Reads to Bypass Recomposition

Jetpack Compose has three phases: **Composition** (what to show), **Layout** (where to place), and **Draw** (how to render). Reading state in Composition triggers all three phases. Reading state in Layout or Draw bypasses earlier phases.

#### A. Animating Layout Positions (Layout-Phase)
* **Redundant (Recomposes Box host on every animation frame):**
```kotlin
val translationX by animateDpAsState(targetValue = targetOffset)
Box(
    modifier = Modifier
        .size(100.dp)
        .offset(x = translationX, y = 0.dp)
)
```
* **Optimized (0 Recompositions, Layout-phase Only):**
```kotlin
val translationX by animateDpAsState(targetValue = targetOffset)
Box(
    modifier = Modifier
        .size(100.dp)
        .offset { IntOffset(x = translationX.roundToPx(), y = 0) } // Defers read
)
```

#### B. Animating Drawing Properties (Draw-Phase)
* **Redundant (Recomposes host and triggers layout):**
```kotlin
val animatedAlpha by animateFloatAsState(targetValue = 0.5f)
Box(
    modifier = Modifier
        .size(100.dp)
        .alpha(animatedAlpha)
)
```
* **Optimized (0 Recompositions, Draw-phase Only):**
```kotlin
val animatedAlpha by animateFloatAsState(targetValue = 0.5f)
Box(
    modifier = Modifier
        .size(100.dp)
        .graphicsLayer { alpha = animatedAlpha } // Direct draw-phase read
)
```

---

### 2. Buffering High-Frequency State (derivedStateOf)

Use `derivedStateOf` when a composable reads state that changes at high frequency (like scroll offset or window size), but you only want to trigger UI updates when a specific threshold/condition is met.

#### Lazy List Scroll Progress
* **Redundant (Recomposes on every single pixel scroll):**
```kotlin
val listState = rememberLazyListState()
val showScrollToTopButton = listState.firstVisibleItemIndex > 0
```
* **Optimized (Recomposes ONLY when the index crosses 0):**
```kotlin
val listState = rememberLazyListState()
val showScrollToTopButton by remember {
    derivedStateOf { listState.firstVisibleItemIndex > 0 }
}
```

---

### 3. Compose Compiler Stability & Reports

#### Fixing Unstable Parameters
Standard Kotlin Collections (`List`, `Map`, `Set`) are treated as unstable because the compiler cannot guarantee their implementations are immutable.

* **Stable Option 1: Immutable Collections (kotlinx-immutable):**
```kotlin
@Composable
fun UserList(users: PersistentList<User>) { // Stable type
    LazyColumn { items(users) { ... } }
}
```
* **Stable Option 2: Stable UI Wrapper Class:**
```kotlin
@Immutable
data class UserListWrapper(val users: List<User>)

@Composable
fun UserList(wrapper: UserListWrapper) { // Wrapper is stable
    LazyColumn { items(wrapper.users) { ... } }
}
```

#### Configuring Compiler Stability Reports
Add this to your module's `build.gradle.kts` to output stability diagnostics to `<module>/build/compose_metrics/`:
```kotlin
composeCompiler {
    enableMetrics.set(true)
    enableReports.set(true)
}
```

---

### 4. Lazy List Recycling Optimization

#### Explicit List Keys
* **Optimized (Prevents index shift recompositions):**
```kotlin
LazyColumn {
    items(
        items = usersList,
        key = { user -> user.uniqueId }
    ) { user ->
        UserCard(user)
    }
}
```

#### List Item Content Types
* **Optimized (Recycles matches by card types):**
```kotlin
LazyColumn {
    items(
        items = feedItems,
        key = { item -> item.id },
        contentType = { item -> item.type }
    ) { item ->
        when (item.type) {
            FeedItemType.CARD -> UserCard(item)
            FeedItemType.AD -> AdBanner(item)
        }
    }
}
```

---

## 📚 Level Up Your Development:
If you are looking for complete, step-by-step implementations, architectural sequence diagrams, and pre-configured template zip files, check out our premium guides:

* [👉 **Jetpack Compose Cookbook (₹299)**](https://yogirana.gumroad.com/l/sriav) — 12 advanced, production-grade UI recipes: collapsing nested-scroll headers, staggered grids, spring-physics swipe actions, shimmers, and gestures.
* [👉 **Advanced Canvas & Custom UI Masterclass (₹1,499)**](https://yogirana.gumroad.com/l/arjjrq) — 37-page print-ready handbook covering geometry path math, velocity tracker knobs, joysticks, subcompose layouts, and recomposition-free GPU drawing.
