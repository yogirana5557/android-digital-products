# Question 5: What is a companion object in Kotlin, and how does it differ from a standard object?

**Category:** Kotlin & Core Java  
**Difficulty:** Mid

---

### Answer

* An `object` in Kotlin defines a singleton class.
* A `companion object` is declared inside a class and is tied to the lifecycle of that class. Members of a companion object can be accessed directly using the class name, similar to `static` members in Java.
```kotlin
class MyClass {
    companion object {
        fun create() = MyClass()
    }
}
val instance = MyClass.create() // Access via class name
```

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
