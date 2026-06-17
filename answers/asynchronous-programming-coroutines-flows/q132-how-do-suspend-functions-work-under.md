# Question 132: How do suspend functions work under the hood in Kotlin?

**Category:** Asynchronous Programming (Coroutines & Flows)  
**Difficulty:** Mid

---

### Answer

Suspend functions are compiled using the **CPS (Continuation-Passing Style)** transformation. The compiler adds an extra parameter of type `Continuation<T>` to the function arguments. The function is compiled into a state machine. When suspended, the function returns a special token (`COROUTINE_SUSPENDED`), releasing the execution thread. When the work is complete, the continuation's `resumeWith()` is called to restore execution state.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
