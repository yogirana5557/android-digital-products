# ⚡ Android Performance Optimization & Profiling Playbook (Free Sample & Checklist)

Welcome to the open-source sample repository and study checklist for the **Android Performance Optimization & Profiling Playbook (Senior Developer's Guide)**.

This handbook is designed for senior and lead Android software engineers who want to build zero-lag apps, optimize battery usage, profile native execution using Perfetto, resolve memory leaks, tune Jetpack Compose recomposition cycles, and minimize app sizes.

---

## 🛍️ Get the Full Playbook (₹699 / ₹799)
If you find this checklist and sample helpful, you can purchase the complete compiled, ad-free PDF eBook containing all 12 chapters, diagrams, and blueprints:
* [👉 **Buy the PDF Playbook on Gumroad (₹699 Launch Deal)**](https://yogirana.gumroad.com/l/fgscvl) *(Includes print-ready PDF, vector flowcharts, and lifetime updates)*

---

## 📋 The 12-Topic Performance Checklist

Use this checklist to track your learning progress or prepare for senior engineering system design and performance interviews:

### 🧠 Chapter 1: Advanced Memory Profiling & Leak Debugging
* [ ] **Topic 1**: Memory Churn, GC Pauses, and the Object Pool Pattern
* [ ] **Topic 2**: Manual Heap Dump Analysis with MAT and GC Roots
* [ ] **Topic 3**: Reference Queues and LruCache Memory Management

### ⚙️ Chapter 2: CPU, Concurrency & Render Profiling
* [ ] **Topic 4**: Thread Lock Contention, Priority Inversion, and Lock-Free Operations
* [ ] **Topic 5**: Frame Render Pipeline, Choreographer, and View Measure Pass Caching
* [ ] **Topic 6**: Cold Startup Optimization with App Startup and Macrobenchmark Testing

### 🎨 Chapter 3: Jetpack Compose Performance Deep Dive
* [x] **Topic 7**: Compose Compiler Reports, Unstable Classes, and Recomposition Skipping *(Read Free Sample Below)*
* [ ] **Topic 8**: State Read Deferral and Layout Phase Optimization
* [ ] **Topic 9**: Lazy List Optimization, DerivedStateOf, and Content Types

### 📦 Chapter 4: Dex Compilation, R8 & Size Hardening
* [ ] **Topic 10**: ProGuard & R8 Optimization Configurations
* [ ] **Topic 11**: Automated Baseline Profile Engineering
* [ ] **Topic 12**: DEX Layout Optimization and Resource Shrinking

---

## 📖 Free Chapter Sample: Topic 7 (Compose Compiler Reports & Stability)

### The Performance Challenge
Declaring list models or custom data classes as standard Kotlin structures often marks them as "unstable" by the Compose Compiler. When a parent composable recomposes, Compose cannot prove that unstable arguments haven't changed. As a result, it forces all children that consume these arguments to recompose redundantly, causing massive frame drops (jank) during list scrolling.

### The Optimization Solution
Run the Compose compiler metrics task in your build process to generate and parse `stability.txt`. Identify unstable variables and enforce compile-time stability by applying `@Stable` or `@Immutable` annotations, wrapping unstable third-party models in a stable container, or using Kotlinx Immutable Collections.

### Production-Grade Code Blueprint
```kotlin
// 1. UNSTABLE PATTERN: Triggers redundant recompositions during list scrolling
// Lists are unstable by default because their contents are mutable.
data class UnstableUser(
    val id: String,
    val name: String,
    val hobbies: List<String> // Declared as standard List -> Unstable!
)

@Composable
fun UnstableUserItem(user: UnstableUser) {
    Text(text = "${user.name} - ${user.hobbies.size}")
}

// 2. OPTIMIZED PATTERN: Stable & Immutable Declarations
// Enforce compile-time stability constraints on the class
@Immutable
data class StableUser(
    val id: String,
    val name: String,
    // Use Kotlinx Immutable collections to guarantee stability
    val hobbies: ImmutableList<String> 
)

@Composable
fun StableUserItem(user: StableUser) {
    Text(text = "${user.name} - ${user.hobbies.size}")
}

// 3. Alternative wrapping of unstable third-party models
@Stable
class StableWrapper<T>(val value: T) {
    override fun equals(other: Any?): Boolean {
        if (this === other) return true
        if (other !is StableWrapper<*>) return false
        return value == other.value
    }
    override fun hashCode(): Int = value?.hashCode() ?: 0
}
```

### Under-The-Hood Architectural Analysis
1. **Smart Recomposition Skipping**: Composable functions are classified as *skippable* or *restartable* by the compiler. A skippable composable does not execute its body if its inputs are structurally equal to their previous state. However, if any input is marked as *unstable*, Compose bypasses equality checks and always recomposes, which wastes CPU cycles during scroll events.
2. **Compiler Stability Criteria**: A class is stable if: 1) all public properties are immutable (declared with `val`), 2) properties are of stable types (primitives, String, other stable classes), and 3) the class notifies Compose when properties change. Standard collections (`List`, `Map`) are interfaces and can point to mutable structures, making them unstable.
3. **Generating Stability Reports**: To inspect class stability, configure the compiler flag `composeCompiler.reportsDestination` in your Gradle script. The output contains a `stability.txt` file detailing every class in the module, marking them as either `stable` or `unstable`, along with a list of unstable properties.
4. **@Stable vs. @Immutable semantics**: `@Immutable` is a strong promise to the compiler that all fields will NEVER change after object creation. `@Stable` allows fields to mutate, provided that the class notifies the Compose runtime when updates occur (e.g. wrapping properties in `State`).

---

## ⚡ Get the Full Playbook
Access all **12 advanced performance chapters** complete with diagrams, profiling steps, and blueprints:
* [👉 **Buy the PDF Playbook on Gumroad (₹699 Launch Deal)**](https://yogirana.gumroad.com/l/fgscvl)
