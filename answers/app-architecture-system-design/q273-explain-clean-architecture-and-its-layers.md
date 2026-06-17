# Question 273: Explain Clean Architecture and its layers.

**Category:** App Architecture & System Design  
**Difficulty:** Senior

---

### Answer

Clean Architecture structures code into circular layers where dependencies point only inwards, decoupling business logic from databases and frameworks:* **Presentation Layer**: UI elements, ViewModels, and Compose layouts.
* **Domain Layer**: Pure Kotlin/Java business rules. Contains **Entities** and **Use Cases**. Has zero Android dependencies.
* **Data Layer**: Database caches, network API interfaces, repositories, and device sensors.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
