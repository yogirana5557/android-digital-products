# Question 1: What is the difference between val and var in Kotlin?

**Category:** Kotlin & Core Java  
**Difficulty:** Junior

---

### Answer

* `val` (Value): Declares a read-only (immutable) variable. Once assigned, its value cannot be changed. It is equivalent to a `final` variable in Java.
* `var` (Variable): Declares a mutable variable. Its value can be reassigned multiple times after initialization.
```kotlin
val name = "Android" // Cannot be reassigned
var version = 14
version = 15 // Allowed
```

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
