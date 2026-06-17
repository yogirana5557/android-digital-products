# Question 174: What is the purpose of @HiltAndroidApp and @AndroidEntryPoint?

**Category:** Dependency Injection (Hilt, Dagger 2)  
**Difficulty:** Mid

---

### Answer

* `@HiltAndroidApp`: Triggers Hilt's code generation. Must be annotated on the custom `Application` class. It sets up the Hilt Singleton Component.
* `@AndroidEntryPoint`: Generates individual dependency injection components for Android classes (Activities, Fragments, Views, Services, Broadcast Receivers), enabling field injection inside them.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
