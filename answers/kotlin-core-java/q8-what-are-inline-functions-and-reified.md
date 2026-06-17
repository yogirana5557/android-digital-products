# Question 8: What are inline functions and reified type parameters in Kotlin?

**Category:** Kotlin & Core Java  
**Difficulty:** Senior

---

### Answer

* **Inline functions**: Tell the compiler to copy the function bytecode directly into the call site rather than generating a function call wrapper. This reduces memory and call-stack overhead when passing lambdas.
* **reified parameters**: Because Java/Kotlin type information is erased at runtime, you normally cannot access a generic type's class inside a function. Marking a generic type parameter as `reified` within an `inline` function preserves the type information at runtime.
```kotlin
inline fun &lt;reified T&gt; checkType(value: Any) {
    if (value is T) {
        println("Value matches type!")
    }
}
```

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
