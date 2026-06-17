# Question 114: What is State Hoisting in Jetpack Compose?

**Category:** State Management & Jetpack Compose  
**Difficulty:** Mid

---

### Answer

State Hoisting is a pattern of moving state up to a composable's caller to make the composable **stateless**. This is achieved by passing the state as a parameter and handling events via callbacks. Stateless composables are easier to test, reuse, and debug.```kotlin
@Composable
fun Counter(count: Int, onIncrement: () -> Unit) {
    Button(onClick = onIncrement) { Text("Count: $count") }
}
```

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
