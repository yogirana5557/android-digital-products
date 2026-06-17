# Question 135: Explain Job vs SupervisorJob in Kotlin Coroutines.

**Category:** Asynchronous Programming (Coroutines & Flows)  
**Difficulty:** Senior

---

### Answer

They differ in how exceptions propagate to sibling tasks:* `Job`: If any child coroutine fails with an exception, the failure cancels the parent job, which automatically cancels all other sibling coroutines in that scope.
* `SupervisorJob`: A failure of one child coroutine does not affect sibling tasks. The supervisor job remains active, enabling individual task failures to be handled locally.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
