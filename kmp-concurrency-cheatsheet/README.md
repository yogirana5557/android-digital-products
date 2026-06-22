# 🚀 Kotlin Multiplatform & Concurrency Developer Cheat Sheet (Free Download)

Welcome to the open-source sample repository and reference checklist for the **Kotlin Multiplatform & Concurrency Developer Cheat Sheet**.

This cheat sheet is a high-performance quick-reference card detailing Kotlin 2.4.0 centralized version catalog configurations, target architectures, Ktor shared engines, Koin injection patterns, Swift coroutines observers, and thread pool dispatch loops.

---

## 🛍️ Get the PDF Edition (Free / $0+)

Get the print-ready, high-resolution 4-page PDF card to keep on your desktop or reference during build configurations:
* [👉 **Download the PDF on Gumroad (Free / $0+)**](https://yogirana.gumroad.com/l/cddkph)

---

## 📋 Cheat Sheet Reference Details

### 1. Centralized Build Setup & Version Catalogs

#### Version Catalog Mappings (`gradle/libs.versions.toml`)
```toml
[versions]
kotlin = "2.4.0"
androidGradlePlugin = "8.4.1"
androidxActivity = "1.9.0"
composeMultiplatform = "1.11.1"
ktor = "3.5.0"
koin = "4.2.2"
room = "2.8.4"
sqlite = "2.5.0-alpha04"
ksp = "2.4.0-1.0.30"

[libraries]
androidx-activity-compose = { module = "androidx.activity:activity-compose", version.ref = "androidxActivity" }
ktor-client-core = { module = "io.ktor:ktor-client-core", version.ref = "ktor" }
ktor-client-okhttp = { module = "io.ktor:ktor-client-okhttp", version.ref = "ktor" }
ktor-client-darwin = { module = "io.ktor:ktor-client-darwin", version.ref = "ktor" }
koin-core = { module = "io.insert-koin:koin-core", version.ref = "koin" }
room-runtime = { module = "androidx.room:room-runtime", version.ref = "room" }
room-compiler = { module = "androidx.room:room-compiler", version.ref = "room" }
sqlite-bundled = { module = "androidx.sqlite:sqlite-bundled", version.ref = "sqlite" }

[plugins]
kotlin-multiplatform = { id = "org.jetbrains.kotlin.multiplatform", version.ref = "kotlin" }
compose-multiplatform = { id = "org.jetbrains.compose", version.ref = "composeMultiplatform" }
kotlin-compose = { id = "org.jetbrains.kotlin.plugin.compose", version.ref = "kotlin" }
room = { id = "androidx.room", version.ref = "room" }
ksp = { id = "com.google.devtools.ksp", version = "2.4.0-1.0.30" }
```

#### Shared Module Configuration (`shared/build.gradle.kts`)
```kotlin
plugins {
    alias(libs.plugins.kotlin.multiplatform)
    alias(libs.plugins.android.library)
    alias(libs.plugins.compose.multiplatform)
    alias(libs.plugins.kotlin.compose) // Compiler plugin mapped to Kotlin version
}

kotlin {
    androidTarget {
        compilerOptions { jvmTarget.set(org.jetbrains.kotlin.gradle.dsl.JvmTarget.JVM_17) }
    }
    listOf(iosX64(), iosArm64(), iosSimulatorArm64()).forEach { target ->
        target.binaries.framework {
            baseName = "SharedFramework"
            isStatic = true // Bypasses codesigning & load-time lookup lags
        }
    }
    sourceSets {
        commonMain.dependencies {
            implementation(libs.ktor.client.core)
            implementation(libs.room.runtime)
            implementation(libs.sqlite.bundled)
        }
        androidMain.dependencies { implementation(libs.ktor.client.okhttp) }
        iosMain.dependencies { implementation(libs.ktor.client.darwin) }
    }
}
```

---

### 2. Shared Clients & Dependency Injection

#### Ktor Shared Engine Factory Setup
```kotlin
// Common Main
class KtorClientFactory(private val engine: HttpClientEngine) {
    fun create(): HttpClient = HttpClient(engine) {
        install(ContentNegotiation) {
            json(Json { ignoreUnknownKeys = true; prettyPrint = true })
        }
    }
}

// Android Main Module Config
val androidHttpClientModule = module {
    single<HttpClientEngine> { OkHttp.create() }
    single { KtorClientFactory(get()).create() }
}

// iOS Main Module Config
val iosHttpClientModule = module {
    single<HttpClientEngine> { Darwin.create() }
    single { KtorClientFactory(get()).create() }
}
```

#### Unified Dependency Injection Modules (Koin DI)
```kotlin
// Common Main - DI Helper initialization function
fun initKoin(appModule: org.koin.core.module.Module) {
    startKoin {
        modules(appModule, commonModule)
    }
}

val commonModule = module {
    single { RoomDatabaseFactory(get()).createRoomDatabase() }
}

// iOS Platform Entrypoint (Swift wrapper calls this)
fun initKoinHelper() = initKoin(module { 
    single<HttpClientEngine> { Darwin.create() } 
})
```

---

### 3. Concurrency, Flows & Platform Observers

#### Swift-Friendly Coroutines Flow Observer Helper
```kotlin
// Common Main - Swift wrapper helper class
class FlowObserver<T>(private val flow: Flow<T>) {
    fun watch(block: (T) -> Unit): Job {
        val scope = CoroutineScope(Dispatchers.Main + SupervisorJob())
        return flow.onEach { block(it) }.launchIn(scope)
    }
}

// Swift UI ViewModel Usage:
watchJob = FlowObserver(flow: usersFlow).watch { users in
    self.usersList = users
}
```

#### Threading & Thread-Pool Allocation Rules
* **Dispatchers.Default**: CPU-bound operations. Thread count capped to CPU cores count (min 2). Deferring state updates prevents UI micro-stutters.
* **Dispatchers.IO**: Disk/network I/O tasks. Defaults to 64 threads or CPU count. Shares thread-pool scheduler with Default.
* **SupervisorJob Exception Boundary**: Child coroutine crash propagates upward. Use `SupervisorJob()` to prevent a single query failure from crashing the entire app.

---

## 📚 Level Up Your Development:
If you are looking for complete, step-by-step implementations, architectural sequence diagrams, and pre-configured template zip files, check out our premium guides:

* [👉 **Kotlin Multiplatform & Compose Cookbook (₹199 / ₹299)**](https://yogirana.gumroad.com/l/oeiqh) — 10 advanced recipes including Room database persistence, Voyager stack navigation, settings caching, and Xcode integration.
* [👉 **Modern Kotlin & Concurrency: Ultimate Prep (₹2,499)**](https://yogirana.gumroad.com/l/czrmy) — 55 senior-level questions, JVM bytecode transformations, structured concurrency exception trees, and scheduler tests.
