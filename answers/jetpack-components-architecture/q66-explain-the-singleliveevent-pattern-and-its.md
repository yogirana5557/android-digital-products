# Question 66: Explain the SingleLiveEvent pattern and its modern alternatives.

**Category:** Jetpack Components & Architecture  
**Difficulty:** Senior

---

### Answer

`SingleLiveEvent` is a custom LiveData subclass used to send one-time events (e.g., showing a Snackbar, navigation) so they are not re-emitted upon configuration changes. In modern Android, developers prefer using Kotlin Coroutine channels or shared flows with a custom event-wrapper to represent one-off UI events.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
