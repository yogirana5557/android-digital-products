# Question 39: Explain the launch modes of Activities: standard, singleTop, singleTask, and singleInstance.

**Category:** Android Basics & Lifecycles  
**Difficulty:** Senior

---

### Answer

Launch modes define how a new instance of an Activity is associated with the current Task:* **standard** (Default): Creates a new instance of the activity in the task from which it was started. Multiple instances can exist in a task.
* **singleTop**: If an instance of the activity already exists at the top of the target task stack, the system routes the intent to that instance via `onNewIntent()` instead of creating a new one.
* **singleTask**: Creates the activity in a new task as root (if not already running). If it already exists in a task, the system brings it to the foreground, destroying all other activities on top of it.
* **singleInstance**: Same as `singleTask`, but the system doesn't launch any other activities into the task holding the instance. The activity is the sole member of its task.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
