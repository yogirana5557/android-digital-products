# 📱 Android Interview Question Bank (2026 Edition)

[![Kotlin](https://img.shields.io/badge/Kotlin-1.9+-7F52FF.svg?style=flat&logo=kotlin)](https://kotlinlang.org)
[![Android](https://img.shields.io/badge/Android-14+-3DDC84.svg?style=flat&logo=android)](https://developer.android.com)
[![Compose](https://img.shields.io/badge/Jetpack_Compose-Premium-4285F4.svg?style=flat&logo=jetpackcompose)](https://developer.android.com/jetpack/compose)
[![eBook](https://img.shields.io/badge/eBook-300_Questions-FF6F61.svg?style=flat&logo=read-the-docs)](#-get-the-full-handbook-pdf)

A comprehensive, highly curated study database of **300 essential Android interview questions and answers**, ranging from Junior to Senior level. Use this repository as a checklist tracker for your interview preparation.

---

## 📖 Get the Full Handbook (PDF)

While this repository provides the complete list of 300 questions and **30 detailed sample answers** (indicated by hyperlinked questions below), the full **250+ page PDF handbook** contains all 300 answers, code snippets, syntax highlighting, and architectural system diagrams.

> [!TIP]
> ### Why get the PDF?
> * **Offline Access**: Learn on the go, anytime.
> * **Beautiful PDF Formatting**: Optimized layout for fast reading and scrolling.
> * **Complete 300 Answers**: In-depth explanations with real-world Kotlin/Java code blocks.
> * **No Noise**: Ad-free, print-ready, and searchable.
>
> [👉 **Get the PDF eBook on Gumroad**](https://yogirana.gumroad.com/l/ljzae) *(or download via landing page)*

---

## 🗂️ Interactive Question Checklist

Use this section to track your study progress. Check off items as you master them!

### 01. Kotlin & Core Java

- [ ] [Q-1: What is the difference between val and var in Kotlin?](answers/kotlin-core-java/q1-what-is-the-difference-between-val.md) `Junior` 🌟 *(Free Sample)*
- [ ] Q-2: What is the difference between val and const val? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-3: How does null safety work in Kotlin? Explain safe calls (?.), Elvis operator (?:), and double bang (!!). `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-4: What is the difference between safe cast (as?) and unsafe cast (as)? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-5: What is a companion object in Kotlin, and how does it differ from a standard object?](answers/kotlin-core-java/q5-what-is-a-companion-object-in.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-6: What is a data class in Kotlin? What methods does the compiler generate automatically for it? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-7: Explain Kotlin's Extension Functions. Do they modify the class they extend? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-8: What are inline functions and reified type parameters in Kotlin?](answers/kotlin-core-java/q8-what-are-inline-functions-and-reified.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-9: Explain the difference between Kotlin's Scope Functions: let, run, apply, also, and with. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-10: What is the difference between lateinit and lazy initialization in Kotlin? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-11: Explain Delegation in Kotlin (the 'by' keyword) and Property Delegates. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-12: What is a smart cast in Kotlin? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-13: What is the difference between == and === in Kotlin? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-14: What is a high-order function in Kotlin? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-15: Explain Sealed Classes vs Enum Classes. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-16: What is the difference between List and MutableList in Kotlin? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-17: What is the meaning of the 'open' and 'final' keywords in Kotlin class declarations? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-18: Explain flatMap vs map in Kotlin collections. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-19: What is a Coroutine in Kotlin? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-20: Explain Java's volatile keyword and its Kotlin equivalent @Volatile. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-21: What is the difference between String, StringBuilder, and StringBuffer? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-22: Explain Covariance (out) and Contravariance (in) in Kotlin generics. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-23: What are Value Classes (inline classes) in Kotlin? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-24: How does Kotlin achieve interoperability with Java? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-25: Explain the concept of Destructuring Declarations. `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-26: What is the use of @JvmStatic, @JvmOverloads, and @JvmField in Kotlin? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-27: Difference between Array<Int> and IntArray in Kotlin? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-28: What is a coroutine Dispatcher? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-29: How does Kotlin's apply differ from also? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-30: What is a backing field in Kotlin, and how is it used? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 02. Android Basics & Lifecycles

- [ ] [Q-31: What are the four core components of an Android application?](answers/android-basics-lifecycles/q31-what-are-the-four-core-components.md) `Junior` 🌟 *(Free Sample)*
- [ ] Q-32: Explain the Android Activity Lifecycle methods. `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-33: How do you handle configuration changes (like screen rotation) in Android?](answers/android-basics-lifecycles/q33-how-do-you-handle-configuration-changes.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-34: What is the difference between explicit and implicit Intents? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-35: What is the difference between Activity Context and Application Context? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-36: Explain the Fragment Lifecycle and how it relates to the Activity Lifecycle. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-37: What is a RecyclerView, and why is it preferred over ListView? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-38: What is the role of DiffUtil in RecyclerView? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-39: Explain the launch modes of Activities: standard, singleTop, singleTask, and singleInstance.](answers/android-basics-lifecycles/q39-explain-the-launch-modes-of-activities.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-40: What is an ANR? What causes it, and how can you detect and prevent it? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-41: What is the difference between Service and IntentService? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-42: What is the difference between a Started Service and a Bound Service? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-43: Explain Foreground Services and the Android 14 restrictions on them. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-44: What are Broadcast Receivers? Explain the difference between Static and Dynamic registration. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-45: What is a PendingIntent? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-46: What is the difference between ViewBinding and DataBinding? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-47: How do you create a custom View? Explain the key methods involved. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-48: Explain the difference between Android Permissions: Normal, Dangerous, and Signature permissions. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-49: What is Process Death in Android, and how do you test and handle it? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-50: What is the difference between dp, sp, and px in Android? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-51: Explain how the Handler and Looper framework works in Android. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-52: What is the purpose of the AndroidManifest.xml file? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-53: What are Vector Drawables, and what are their advantages? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-54: What is the difference between Style and Theme? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-55: What is a DialogFragment, and why should it be used instead of a bare Dialog? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-56: Explain Deep Links vs App Links in Android. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-57: What is the Backpressure problem in reactive programming, and how is it handled in Flow/RxJava? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-58: Explain the new Splash Screen API introduced in Android 12. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-59: What is the difference between Toast and Snackbar? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-60: How does the Android system manage memory? What happens when memory runs low? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 03. Jetpack Components & Architecture

- [ ] [Q-61: What is Android Jetpack?](answers/jetpack-components-architecture/q61-what-is-android-jetpack.md) `Junior` 🌟 *(Free Sample)*
- [ ] Q-62: What is the purpose of the ViewModel component? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-63: What is LiveData? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-64: What is the difference between setValue() and postValue() in LiveData?](answers/jetpack-components-architecture/q64-what-is-the-difference-between-setvalue.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-65: What is the purpose of MediatorLiveData? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-66: Explain the SingleLiveEvent pattern and its modern alternatives.](answers/jetpack-components-architecture/q66-explain-the-singleliveevent-pattern-and-its.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-67: What is Room Database? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-68: What are the three main components of Room? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-69: What are TypeConverters in Room, and when do you use them? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-70: Explain database migrations in Room. How do AutoMigrations work? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-71: How do you represent one-to-many and many-to-many relationships in Room? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-72: What is WorkManager, and when should it be used? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-73: What is the difference between Worker and CoroutineWorker in WorkManager? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-74: How do you pass input data to a WorkManager task and retrieve output results? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-75: Explain WorkManager's Backoff Policies and Retry mechanisms. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-76: What is the Navigation Component, and what are its key parts? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-77: What are Safe Args in Navigation Component? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-78: How does Navigation Component manage multiple backstacks? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-79: What is DataStore, and why is it preferred over SharedPreferences? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-80: Explain the difference between Preferences DataStore and Proto DataStore. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-81: What is the Paging 3 library, and what is the role of RemoteMediator? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-82: What is App Startup library? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-83: What is the difference between ViewModel and AndroidViewModel? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-84: What is a SavedStateHandle, and when should it be used? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-85: What is a LifecycleObserver? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-86: What is the difference between lifecycleScope and viewModelScope? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-87: How does Room ensure query safety at compile time? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-88: What is an in-memory database in Room, and when is it useful? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-89: What is the purpose of the @Transaction annotation in Room DAOs? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-90: What is the purpose of the onCleared() method in ViewModels? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-91: How does Flow integrate with Room queries? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-92: Explain WorkManager's Expedition Jobs (Expedited Work). `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-93: What is the difference between OneTimeWorkRequest and PeriodicWorkRequest? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-94: What is ViewModels Factory, and why do we need it? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-95: Explain how popUpTo and popUpToInclusive work in Navigation Component. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-96: What are WorkManager constraints? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-97: How do you observe WorkManager job states in UI? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-98: Explain Room AutoMigrations and when they fail. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-99: How does LifecycleEventObserver differ from DefaultLifecycleObserver? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-100: What is the difference between LiveData and Observable (from RxJava)? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-101: What is the role of LifecycleOwner in Android? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-102: What is the purpose of the Room DatabaseBuilder? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-103: Explain how Paging 3 manages data loading states in the UI. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-104: What are the common work states in WorkManager? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-105: How do you migrate SharedPreferences to Preferences DataStore? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-106: Explain how to share ViewModels between Fragments in Android. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-107: What is the purpose of the LiveData transformations map and switchMap? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-108: Can we execute SQL queries dynamically in Room? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-109: How does ProcessLifecycleOwner help track app foreground/background state? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-110: What is a Room Database View, and when is it used? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 04. State Management & Jetpack Compose

- [ ] [Q-111: What is the difference between Imperative UI and Declarative UI?](answers/state-management-jetpack-compose/q111-what-is-the-difference-between-imperative.md) `Junior` 🌟 *(Free Sample)*
- [ ] Q-112: What is Recomposition in Jetpack Compose? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-113: Explain remember, mutableStateOf, and rememberSaveable. `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-114: What is State Hoisting in Jetpack Compose?](answers/state-management-jetpack-compose/q114-what-is-state-hoisting-in-jetpack.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-115: Does the order of Modifiers in Compose matter? Explain with an example. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-116: What are Side-Effects in Compose? Explain LaunchedEffect, DisposableEffect, and SideEffect.](answers/state-management-jetpack-compose/q116-what-are-sideeffects-in-compose-explain.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-117: What is rememberCoroutineScope, and when should you use it? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-118: Explain CompositionLocal and when it should be used. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-119: What is the Compose equivalent of RecyclerView? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-120: Explain Stable vs Immutable types in Compose, and how they affect Recomposition. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-121: What is derivedStateOf, and why is it important for performance? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-122: How do you render a standard Android View inside Jetpack Compose? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-123: What are the three phases of rendering in Jetpack Compose? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-124: What is the Scaffold composable? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-125: What are key components of Compose animations? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-126: Explain Intrinsic Measurements in Jetpack Compose. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-127: What is the slot API pattern in Jetpack Compose? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-128: What is the difference between Column, Row, and Box? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-129: How do you detect memory leaks in Compose UI? What can cause them? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-130: What is the use of the LocalContext CompositionLocal? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-151: What is a Composable function? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-152: What is the default modifier in Jetpack Compose? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-153: What is the purpose of rememberUpdatedState in Compose? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-154: What are custom Modifiers, and how do you build them? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-155: What is a BoxWithConstraints Composable? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-156: What is the role of key in Compose lists? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-157: How do you draw on screen using Canvas in Compose? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-158: Explain how Compose handles touch event dispatching. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-159: What is the difference between Material 2 and Material 3 in Compose? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-160: How do you capture preview views in Compose? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 05. Asynchronous Programming (Coroutines & Flows)

- [ ] [Q-131: What is the difference between launch and async in Coroutines?](answers/asynchronous-programming-coroutines-flows/q131-what-is-the-difference-between-launch.md) `Junior` 🌟 *(Free Sample)*
- [ ] [Q-132: How do suspend functions work under the hood in Kotlin?](answers/asynchronous-programming-coroutines-flows/q132-how-do-suspend-functions-work-under.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-133: What is the difference between blocking and suspending? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-134: What is Structured Concurrency? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-135: Explain Job vs SupervisorJob in Kotlin Coroutines.](answers/asynchronous-programming-coroutines-flows/q135-explain-job-vs-supervisorjob-in-kotlin.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-136: What is a CoroutineContext? What elements does it contain? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-137: How does cancellation work in Coroutines? Why must it be cooperative? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-138: What is the purpose of withContext in Kotlin Coroutines? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-139: Why is runBlocking discouraged in production Android code, and when is it acceptable? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-140: What is a Flow in Kotlin? How does it differ from a standard List? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-141: Explain the difference between Cold Flows and Hot Flows. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-142: What is the difference between StateFlow and SharedFlow? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-143: How do you collect Flows safely in Android UI components? Explain collectAsStateWithLifecycle. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-144: Explain the difference between collect and collectLatest in Kotlin Flow. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-145: Explain flow flatMapLatest, combine, and zip operators. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-146: What is a Channel in Kotlin? How does it differ from a Flow? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-147: What are the common dispatchers provided by Kotlin Coroutines? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-148: Explain how to handle exceptions inside Coroutine scopes. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-149: What is withContext(NonCancellable) and when is it used? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-150: Explain the role of yield() in Kotlin Coroutines. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-161: What does the coroutineScope builder do? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-162: How do you create a Flow? What are the common flow builders? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-163: Explain the difference between flowOn and standard coroutine dispatchers. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-164: What does the shareIn operator do? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-165: Explain Flow's buffer operator. When should it be used? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-166: What is the catch operator in Flow? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-167: What is the difference between launchIn and collect in Flows? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-168: Explain the difference between channelFlow and flow builders. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-169: What does the stateIn operator do? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-170: Why is GlobalScope discouraged in Android development? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 06. Dependency Injection (Hilt, Dagger 2)

- [ ] [Q-171: What is Dependency Injection (DI)? Why is it used?](answers/dependency-injection-hilt-dagger-2/q171-what-is-dependency-injection-di-why.md) `Junior` 🌟 *(Free Sample)*
- [ ] Q-172: What is the difference between Dagger 2 and Hilt? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-173: Explain Constructor Injection vs Field Injection. `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-174: What is the purpose of @HiltAndroidApp and @AndroidEntryPoint?](answers/dependency-injection-hilt-dagger-2/q174-what-is-the-purpose-of-hiltandroidapp.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-175: Explain the difference between @Provides and @Binds inside DI modules. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-176: What are Hilt Components and Scopes? List their hierarchies.](answers/dependency-injection-hilt-dagger-2/q176-what-are-hilt-components-and-scopes.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-177: What are Qualifiers in Dagger/Hilt? When should you use them? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-178: Explain @EntryPoint in Hilt and when it is needed. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-179: Explain AssistInject in Hilt. What problem does it solve? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-180: What is the difference between Lazy<T> and Provider<T> in Dagger? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-181: What are Dagger Multibindings? Explain intoSet and intoMap. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-182: What annotation is used to declare a Dagger Module? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-183: What is the role of the @InstallIn annotation in Hilt? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-184: How do you perform Unit Testing with Hilt? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-185: Why does Hilt validation happen at compile time? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-186: Can Hilt inject dependencies into a ViewModel? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-187: What is @BindsInstance in Dagger? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-188: What is a dependency cycle in DI, and how do you resolve it? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-189: What is the difference between scoped and unscoped bindings in Hilt? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-190: Can a Hilt component inherit dependencies from another Hilt component? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 07. Networking & Data Serialization (Retrofit, OkHttp)

- [ ] [Q-191: What is Retrofit? How does it differ from standard HttpUrlConnection?](answers/networking-data-serialization-retrofit-okhttp/q191-what-is-retrofit-how-does-it.md) `Junior` 🌟 *(Free Sample)*
- [ ] Q-192: What is OkHttp? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-193: What is the difference between Application Interceptors and Network Interceptors in OkHttp?](answers/networking-data-serialization-retrofit-okhttp/q193-what-is-the-difference-between-application.md) `Mid` 🌟 *(Free Sample)*
- [ ] [Q-194: What is SSL Pinning, and how is it implemented in OkHttp?](answers/networking-data-serialization-retrofit-okhttp/q194-what-is-ssl-pinning-and-how.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-195: How do you implement offline caching in OkHttp? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-196: How does Retrofit support Kotlin Coroutines? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-197: Compare GSON, Moshi, and Kotlinx Serialization. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-198: How do you implement dynamic Base URLs in Retrofit? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-199: How do you specify headers in Retrofit calls? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-200: Explain Network Security Config in Android. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-201: What is HttpLoggingInterceptor? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-202: What is the role of Converter.Factory in Retrofit? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-203: Explain OkHttp's Connection Pooling mechanism. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-204: What is the difference between @Path and @Query in Retrofit? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-205: What is a Multipart request in Retrofit? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-206: How do you configure timeouts in Retrofit/OkHttp? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-207: How do you handle API errors gracefully in Retrofit? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-208: How do you handle redirections in OkHttp? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-209: Why should we avoid printing API logs in Production? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-210: Explain OkHttp Authenticator interface. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 08. Memory Management & Performance

- [ ] [Q-211: What is a Memory Leak in Android?](answers/memory-management-performance/q211-what-is-a-memory-leak-in.md) `Junior` 🌟 *(Free Sample)*
- [ ] [Q-212: What are the common causes of memory leaks in Android?](answers/memory-management-performance/q212-what-are-the-common-causes-of.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-213: What is LeakCanary, and how does it work? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-214: Explain Proguard and R8. What is the difference between them?](answers/memory-management-performance/q214-explain-proguard-and-r8-what-is.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-215: What is the purpose of proguard-rules.pro files? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-216: Explain garbage collection in Android. What is ART's CMS vs GC on-demand? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-217: What is App Overdraw? How do you detect and fix it? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-218: What is the Android Profiler, and what metrics does it track? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-219: Explain double taxation in View rendering. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-220: What are App Bundles (.aab), and how do they reduce APK size? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-221: Why is it important to keep the layout hierarchy flat? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-222: What is the purpose of the <merge> tag in layouts? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-223: Explain strictmode in Android development. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-224: What is the target frame rate for smooth animations in Android? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-225: How do you detect memory leaks using Android Studio Profiler? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-226: Explain JVM Garbage Collection roots (GC Roots). `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-227: What is the impact of excessive object allocations in loops? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-228: What is the purpose of the ViewStub component? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-229: How does R8 perform class inlining and optimization? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-230: What is the difference between clean and rebuild in Android Studio? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-231: What is Bitmap pooling? Why is it useful? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-232: Explain the difference between JIT and AOT compilation in Android. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-233: Why should we avoid deep nesting of ConstraintLayout? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-234: How do you analyze APK file size? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-235: Explain VSync and its importance in Android UI. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-236: What is the impact of holding static references to Views? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-237: How does Glide/Coil optimize image loading? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-238: What is profile-guided optimization (PGO) in ART? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-239: What is the purpose of the android:largeHeap attribute? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-240: Explain the difference between cold start, warm start, and hot start. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 09. Testing & Automation

- [ ] [Q-241: What is the difference between Local Unit Tests and Instrumented Tests?](answers/testing-automation/q241-what-is-the-difference-between-local.md) `Junior` 🌟 *(Free Sample)*
- [ ] Q-242: What is the purpose of JUnit in Android testing? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-243: What is Mockito/MockK? Why are they used?](answers/testing-automation/q243-what-is-mockitomockk-why-are-they.md) `Mid` 🌟 *(Free Sample)*
- [ ] Q-244: What is Espresso, and what are its three main components? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] [Q-245: Explain Robolectric and its advantages over standard instrumented tests.](answers/testing-automation/q245-explain-robolectric-and-its-advantages-over.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-246: What is the difference between a Mock, a Spy, and a Fake in testing? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-247: How do you test Kotlin Coroutines? Explain TestScope and runTest. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-248: What is TDD (Test-Driven Development)? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-249: Explain how to test ViewModel state updates. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-250: What is UI Automator, and when should it be used instead of Espresso? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-251: What is code coverage in testing? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-252: What is the purpose of IdlingResources in Espresso? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-253: How do you test Jetpack Compose UI components? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-254: What is assertion in unit testing? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-255: How do you mock final classes in Mockito? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-256: Explain how to override Main Dispatcher in unit tests. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-257: What are flaky tests? How do you prevent them? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-258: What is the purpose of the MockWebServer library? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-259: Explain how to write custom Espresso view matchers. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-260: What is the testing pyramid? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-261: What is the difference between @Before and @BeforeClass in JUnit? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-262: Explain Semantics in Compose Testing. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-263: What does the @Ignore annotation do in JUnit? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-264: How do you test Room database operations? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-265: Explain the difference between mockk and coEvery in MockK. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-266: What is regression testing? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-267: How do you test dynamic permissions in Espresso? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-268: What is the Android Test Orchestrator? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-269: What is assertions library Truth? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-270: Explain how to write screenshot tests in Android. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

### 10. App Architecture & System Design

- [ ] [Q-271: What is MVVM architecture?](answers/app-architecture-system-design/q271-what-is-mvvm-architecture.md) `Junior` 🌟 *(Free Sample)*
- [ ] [Q-272: What is MVI architecture? How does it differ from MVVM?](answers/app-architecture-system-design/q272-what-is-mvi-architecture-how-does.md) `Mid` 🌟 *(Free Sample)*
- [ ] [Q-273: Explain Clean Architecture and its layers.](answers/app-architecture-system-design/q273-explain-clean-architecture-and-its-layers.md) `Senior` 🌟 *(Free Sample)*
- [ ] Q-274: What is the Repository Pattern? What problem does it solve? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-275: Explain the role of Use Cases (Interactors) in Clean Architecture. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-276: What is Gradle in Android development? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-277: What are Build Types vs Product Flavors in Gradle? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-278: Explain Gradle Kotlin DSL and its advantages over Groovy DSL. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-279: What is the purpose of the Android Keystore System? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-280: Explain modularization in Android. What are its benefits? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-281: What is a singleton pattern? How is it implemented in Kotlin? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-282: What are Gradle dependency configurations: api vs implementation? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-283: What is Gradle Configuration Cache? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-284: What is the purpose of settings.gradle file? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-285: How do you securely store API keys in Android apps? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-286: Explain SQL Injection in Android SQLite. How do you prevent it? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-287: What is the difference between compileSdk and targetSdk? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-288: Explain dependency version catalogs in Gradle. `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-289: What is offline-first architecture? How do you implement it? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-290: What is the role of minSdk in Android? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-291: How does the Gradle build cache work? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-292: Explain the difference between OAuth 2 and API Keys in mobile client security. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-293: What is clean architecture Domain layer? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-294: What is a custom Gradle task? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-295: Explain App Sandboxing in Android. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-296: What is the purpose of local.properties file? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-297: What is proguard mapping file? Why is it needed? `Mid` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-298: What is dynamic delivery in Android? `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-299: What is the purpose of the build.gradle file? `Junior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*
- [ ] Q-300: Explain how to secure local SQLite database files in Android. `Senior` — *[Answer in PDF](#-get-the-full-handbook-pdf)*

---

## 🚀 How to Use this Repository

1. **Fork this repository** to your account.
2. **Use it as a Study Planner**: Mark questions from `[ ]` to `[x]` as you master the concepts.
3. **Contribute**: Found an issue, or want to suggest a new advanced question? Feel free to submit a Pull Request!

## 📄 License & Terms

* The markdown question lists and sample answers in this repository are licensed under the **MIT License**.
* The compiled **Android Interview Question Bank PDF** is copyrighted material and may not be redistributed or resold without explicit permission.

---
*Created with ❤️ by Yadnyesh Rana. Good luck with your interview preparation!*
