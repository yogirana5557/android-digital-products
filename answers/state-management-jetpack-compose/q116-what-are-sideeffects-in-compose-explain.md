# Question 116: What are Side-Effects in Compose? Explain LaunchedEffect, DisposableEffect, and SideEffect.

**Category:** State Management & Jetpack Compose  
**Difficulty:** Senior

---

### Answer

Side-effects are operations that escape the scope of a composable function (e.g., fetching network data, analytical logging).* `LaunchedEffect`: Runs a suspend function within a coroutine scope. It is triggered when first entering composition and restarts whenever its key parameters change.
* `DisposableEffect`: Used for side effects that require cleanups (e.g. unregistering listeners). It provides an `onDispose` block triggered when leaving composition.
* `SideEffect`: Executes a non-suspending block after **every successful recomposition** to publish state updates to non-compose objects.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
