# 🧪 Android & Compose Testing Playbook (Free Sample & Checklist)

Welcome to the open-source sample repository and study checklist for the **Android & Compose Testing Playbook: Unit, UI & Integration Testing Mastery**.

This handbook is designed for senior and lead Android software engineers who want to build a test suite the whole team actually trusts — covering JUnit5 and MockK fundamentals, testing Kotlin Flows and StateFlow with Turbine, Jetpack Compose UI testing, Hilt and Room integration testing, and the CI strategy that keeps a growing suite fast instead of flaky.

---

## 🛍️ Get the Full Playbook (₹599)
If you find this checklist and sample helpful, you can purchase the complete compiled, ad-free PDF eBook containing all 12 topics, code blueprints, and architectural breakdowns:
* [👉 **Buy the PDF Playbook on Gumroad (₹599)**](https://yogirana.gumroad.com/l/android-testing-playbook) *(Includes print-ready PDF and lifetime updates)*

---

## 📋 The 12-Topic Testing Checklist

Use this checklist to track your learning progress or shore up your testing knowledge before a senior engineering interview:

### 🧱 Chapter 1: Unit Testing Foundations
* [ ] **Topic 1**: JUnit5 Architecture, Parameterized Tests & the Test Double Spectrum
* [ ] **Topic 2**: Mocking with MockK: Relaxed Mocks, Slots & Coroutine-Aware Verification
* [ ] **Topic 3**: Testing Kotlin Flows & StateFlow with Turbine

### 🎨 Chapter 2: Jetpack Compose UI Testing
* [ ] **Topic 4**: ComposeTestRule Fundamentals: The Semantics Tree, Finders & Synchronization
* [ ] **Topic 5**: Custom Semantics, testTag Strategy & Merging Semantics Nodes
* [ ] **Topic 6**: Testing Gestures, Animations & Idling Resources

### 🏗️ Chapter 3: Architecture & Integration Testing
* [x] **Topic 7**: Testing StateFlow-Driven ViewModels: Turbine + Fake Repositories *(Read Free Sample Below)*
* [ ] **Topic 8**: Hilt Test Modules: @TestInstallIn, @BindValue & Swapping Dependencies
* [ ] **Topic 9**: Room Database Testing: In-Memory Databases, Migrations & DAO Contracts

### 🚦 Chapter 4: Test Strategy, CI & Reliability
* [ ] **Topic 10**: The Android Test Pyramid: Balancing Unit, Integration & E2E Coverage
* [ ] **Topic 11**: Diagnosing & Eliminating Flaky Tests: Dispatchers, Clocks & IdlingResources
* [ ] **Topic 12**: CI Test Matrices: Sharding, Parallelization & Coverage Gates

---

## 📖 Free Chapter Sample: Topic 7 (Testing StateFlow-Driven ViewModels)

### The Testing Challenge
Modern `ViewModel`s expose a single `StateFlow<UiState>` built by combining multiple upstream flows, often behind `stateIn(scope, SharingStarted.WhileSubscribed(5000), initialValue)`. Testing this correctly is where most teams stumble: they either mock the repository so heavily that the test verifies the mock's configuration rather than the ViewModel's actual reducer logic, or they get bitten by `WhileSubscribed`'s lazy activation and see the flow never emit at all in the test.

### The Solution
Back the repository dependency with a hand-written **fake** — an in-memory implementation exposing a `MutableStateFlow` the test can push values into directly — and use Turbine's `test {}` to collect the ViewModel's public state, driving the fake's flow and asserting on each resulting state transition in sequence.

### Production-Grade Code Blueprint
```kotlin
// A fake, not a mock: real (if simplified) behavior, no verify() needed
class FakeOrdersRepository : OrdersRepository {
    val ordersFlow = MutableStateFlow<List<Order>>(emptyList())
    override fun observeOrders(): Flow<List<Order>> = ordersFlow
}

class OrdersViewModel(
    repository: OrdersRepository,
    scope: CoroutineScope = viewModelScope,
) {
    val state: StateFlow<OrdersUiState> = repository.observeOrders()
        .map { orders ->
            if (orders.isEmpty()) OrdersUiState.Empty
            else OrdersUiState.Loaded(orders.sortedByDescending { it.placedAt })
        }
        .stateIn(scope, SharingStarted.WhileSubscribed(5000), OrdersUiState.Loading)
}

class OrdersViewModelTest {

    private val fakeRepository = FakeOrdersRepository()
    private lateinit var viewModel: OrdersViewModel

    @Test
    fun `emits Loading then Empty when repository starts with no orders`() = runTest {
        viewModel = OrdersViewModel(fakeRepository, scope = backgroundScope)

        viewModel.state.test {
            assertEquals(OrdersUiState.Loading, awaitItem())
            assertEquals(OrdersUiState.Empty, awaitItem())
        }
    }

    @Test
    fun `sorts newly emitted orders by most recent first`() = runTest {
        viewModel = OrdersViewModel(fakeRepository, scope = backgroundScope)

        viewModel.state.test {
            awaitItem() // Loading
            awaitItem() // Empty (initial flow value)

            fakeRepository.ordersFlow.value = listOf(
                Order(id = "o1", placedAt = 100L),
                Order(id = "o2", placedAt = 300L),
            )

            val loaded = awaitItem() as OrdersUiState.Loaded
            assertEquals(listOf("o2", "o1"), loaded.orders.map { it.id })
        }
    }
}
```

### Under-The-Hood Architectural Analysis
1. **`backgroundScope` solves the `WhileSubscribed` trap.** `runTest`'s own coroutine scope completes as soon as the test body returns, which cancels a `stateIn` flow scoped to it *before* Turbine can collect anything meaningful if you're not careful with ordering. `backgroundScope` — provided by `kotlinx-coroutines-test` — lives for the duration of the whole test and is automatically cancelled after, which is the correct scope to hand a `ViewModel` under test so `WhileSubscribed` behaves the same way it would with a real `viewModelScope`.
2. **Fakes verify behavior; mocks verify interactions.** The `FakeOrdersRepository` test above never calls `verify { repository.observeOrders() }` — it doesn't need to, because pushing a real value into `ordersFlow` and observing the resulting `state` transition *is* the verification. This makes the test resilient to refactors that change *how* the ViewModel calls the repository, as long as the observable behavior is unchanged.
3. **Why the first assertion is `Loading`, not `Empty`.** `stateIn` emits its `initialValue` synchronously to the first collector, *then* starts collecting the upstream flow, which itself has a `MutableStateFlow` default of `emptyList()` that immediately maps to `Empty`. Missing this two-step emission sequence is the single most common cause of "my Turbine test times out on `awaitItem()`" bug reports.
4. **`SharingStarted.WhileSubscribed(5000)` vs `Eagerly` in tests.** With `WhileSubscribed`, the upstream flow doesn't start collecting until something subscribes to `state` — which is exactly what `viewModel.state.test {}` does. If your test asserts against `viewModel.state.value` directly (a plain property read) instead of going through `.test {}`, you may read a stale or default value because nothing has subscribed yet to trigger the lazy start.

---

## 🧪 Get the Full Playbook
Access all **12 testing topics** across unit, UI, and integration testing, complete with production-grade code blueprints and under-the-hood analysis:
* [👉 **Buy the PDF Playbook on Gumroad (₹599)**](https://yogirana.gumroad.com/l/android-testing-playbook)
