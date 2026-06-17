# Question 272: What is MVI architecture? How does it differ from MVVM?

**Category:** App Architecture & System Design  
**Difficulty:** Mid

---

### Answer

MVI (Model-View-Intent) enforces unidirectional data flow:* **Intent**: Represents user actions (not Android Intents).
* **Model**: Represents immutable state.
* **View**: Renders the state.
Unlike MVVM (which can have multiple state streams), MVI consolidates UI state into a **single immutable state object** that is updated via actions, preventing inconsistent UI states.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
