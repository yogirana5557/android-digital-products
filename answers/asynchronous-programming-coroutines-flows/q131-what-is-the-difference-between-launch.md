# Question 131: What is the difference between launch and async in Coroutines?

**Category:** Asynchronous Programming (Coroutines & Flows)  
**Difficulty:** Junior

---

### Answer

Both start a new coroutine, but return different handle objects:* `launch`: Used for 'fire-and-forget' tasks. It returns a `Job` object and does not return any computation result. Exception failures propagate immediately.
* `async`: Used for computing results. It returns a `Deferred<T>` object (subclass of Job). Callers call `await()` to retrieve the computed value. Exceptions are packaged inside the Deferred object and thrown when calling await.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
