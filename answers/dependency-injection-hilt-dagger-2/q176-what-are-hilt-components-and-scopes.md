# Question 176: What are Hilt Components and Scopes? List their hierarchies.

**Category:** Dependency Injection (Hilt, Dagger 2)  
**Difficulty:** Senior

---

### Answer

Hilt provides built-in components that manage the lifecycles of injected bindings. Scopes bind instances to the lifetime of their corresponding components:<table border='1' style='border-collapse:collapse; width:100%; text-align:left; margin-top:10px;'><tr><th>Component</th><th>Scope Annotation</th><th>Created / Destroyed Event</th></tr><tr><td>`SingletonComponent`</td><td>`@Singleton`</td><td>App startup / App shutdown</td></tr><tr><td>`ActivityRetainedComponent`</td><td>`@ActivityRetainedScoped`</td><td>Activity first create / survives config changes / destroyed on process death</td></tr><tr><td>`ViewModelComponent`</td><td>`@ViewModelScoped`</td><td>ViewModel creation / ViewModel cleared</td></tr><tr><td>`ActivityComponent`</td><td>`@ActivityScoped`</td><td>Activity onCreate / Activity onDestroy</td></tr><tr><td>`FragmentComponent`</td><td>`@FragmentScoped`</td><td>Fragment onAttach / Fragment onDestroy</td></tr></table>

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
