# Question 33: How do you handle configuration changes (like screen rotation) in Android?

**Category:** Android Basics & Lifecycles  
**Difficulty:** Mid

---

### Answer

When a configuration change occurs (rotation, language change), Android destroys and recreates the active Activity to load resources matching the new config.To handle this without losing user state:* Use a **ViewModel** to store UI-related data. ViewModels survive configuration changes.
* Use `SavedStateHandle` or `onSaveInstanceState()` to preserve small, essential system-level states (like input field values or list scroll positions) across process death.
* Avoid using `android:configChanges` in the manifest to bypass rotation recreation, as it forces you to handle all resource updates manually.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
