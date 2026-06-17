# Question 64: What is the difference between setValue() and postValue() in LiveData?

**Category:** Jetpack Components & Architecture  
**Difficulty:** Mid

---

### Answer

* `setValue()`: Updates the LiveData value on the **Main Thread**. It must be called from the main thread; calling it from a background thread throws an exception.
* `postValue()`: Updates the LiveData value from a **Background Thread**. Under the hood, it posts a runnable task to the main thread's message queue to set the value.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
