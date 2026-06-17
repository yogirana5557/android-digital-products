# Question 212: What are the common causes of memory leaks in Android?

**Category:** Memory Management & Performance  
**Difficulty:** Mid

---

### Answer

Common causes include:* Passing Activity Context to singleton classes or static variables.
* Keeping references to Views in Fragments after `onDestroyView()`.
* Not canceling Coroutine jobs or RxJava subscriptions when a component is destroyed.
* Non-static inner classes (like Handler or Thread) holding implicit references to the outer Activity.
* Registering listeners/callbacks (like location updates) and forgetting to unregister them.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
