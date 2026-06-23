# 🚀 Android System Design & Architecture Checklist (Free Download)

Welcome to the open-source sample repository and reference checklist for the **Android System Design & Architecture Checklist**.

This checklist is a high-performance 12-page reference card detailing multi-module configurations, precompiled convention plugins, offline-first data synchronization, Room mutations write-queues, SQLCipher local encryption, Trusted Execution Environment (TEE) Keystore keys, and thread-safe token bucket rate limiters.

---

## 🛍️ Get the PDF Edition (Free / $0+)

Get the print-ready, high-resolution 12-page PDF handbook to keep on your desktop or reference during architecture reviews:
* [👉 **Download the PDF on Gumroad (Free / $0+)**](https://yogirana.gumroad.com/l/system-design-checklist) *(Use this link to download the PDF, enter 0 to get it free!)*

---

## 📋 Checklist Reference Details

### 1. Multi-Module Monorepo Setup

#### A. Centralized Version Catalog (`gradle/libs.versions.toml`)
```toml
[versions]
kotlin = "2.4.0"
androidGradlePlugin = "8.4.1"
ktor = "3.5.0"
koin = "4.2.2"
room = "2.8.4"
sqlite = "2.5.0-alpha04"

[libraries]
ktor-client-core = { module = "io.ktor:ktor-client-core", version.ref = "ktor" }
ktor-client-okhttp = { module = "io.ktor:ktor-client-okhttp", version.ref = "ktor" }
koin-core = { module = "io.insert-koin:koin-core", version.ref = "koin" }
room-runtime = { module = "androidx.room:room-runtime", version.ref = "room" }
sqlite-bundled = { module = "androidx.sqlite:sqlite-bundled", version.ref = "sqlite" }

[plugins]
kotlin-multiplatform = { id = "org.jetbrains.kotlin.multiplatform", version.ref = "kotlin" }
room = { id = "androidx.room", version.ref = "room" }
```

#### B. Precompiled Gradle Convention Plugins (`build-logic`)
```kotlin
// /build-logic/convention/src/main/kotlin/AndroidLibraryConventionPlugin.kt
class AndroidLibraryConventionPlugin : Plugin<Project> {
    override fun apply(target: Project) {
        with(target) {
            with(pluginManager) {
                apply("com.android.library")
                apply("org.jetbrains.kotlin.android")
            }
            extensions.configure<LibraryExtension> {
                compileSdk = 34
                defaultConfig { minSdk = 26 }
                compileOptions {
                    sourceCompatibility = JavaVersion.VERSION_17
                    targetCompatibility = JavaVersion.VERSION_17
                }
            }
        }
    }
}
```

#### C. Unidirectional Module Dependencies
1. **app module**: Applies all features. Knows nothing of feature internals.
2. **feature modules**: Depend on core layers. Features never depend directly on other features.
3. **api vs implementation**: Use `api` dependencies for types exposed in a module's public interfaces (like models). Use `implementation` for internal layers (like Ktor engines).

---

### 2. Offline-First: Network-Bound Resource (NBR)

Display cached data immediately while running network fetches in the background. Use Room as the Single Source of Truth (SSOT).

```kotlin
inline fun <ResultType, RequestType> networkBoundResource(
    crossinline query: () -> Flow<ResultType>,
    crossinline fetch: suspend () -> RequestType,
    crossinline saveFetchResult: suspend (RequestType) -> Unit,
    crossinline shouldFetch: (ResultType) -> Boolean = { true }
) = flow {
    emit(Resource.Loading(null))
    val data = query().first()

    if (shouldFetch(data)) {
        emit(Resource.Loading(data))
        try {
            val fetchedResult = fetch()
            saveFetchResult(fetchedResult)
            emitAll(query().map { Resource.Success(it) })
        } catch (throwable: Throwable) {
            emitAll(query().map { Resource.Error(throwable, it) })
        }
    } else {
        emitAll(query().map { Resource.Success(it) })
    }
}
```

---

### 3. Room Transaction Write-Queues & Background Syncing

#### A. Mutation Queue Entity
```kotlin
@Entity(tableName = "mutation_queue")
data class PendingMutation(
    @PrimaryKey(autoGenerate = true) val id: Long = 0,
    val type: String, // "INSERT", "UPDATE", "DELETE"
    val targetTable: String,
    val payloadJson: String, // Serialized payload values
    val timestamp: Long = System.currentTimeMillis()
)
```

#### B. Sync Worker & Scheduling Configuration
```kotlin
class SyncWorker(
    context: Context,
    params: WorkerParameters,
    private val db: AppDatabase,
    private val api: KtorClient
) : CoroutineWorker(context, params) {
    override suspend fun doWork(): Result {
        val pending = db.mutationDao().getAllPending()
        if (pending.isEmpty()) return Result.success()
        for (mutation in pending) {
            try {
                val res = api.syncMutation(mutation.type, mutation.payloadJson)
                if (res.status.value in 200..299) db.mutationDao().delete(mutation)
            } catch (e: Exception) { return Result.retry() }
        }
        return Result.success()
    }
}

// Scheduling WorkManager with Constraints
val constraints = Constraints.Builder().setRequiredNetworkType(NetworkType.CONNECTED).build()
val syncRequest = OneTimeWorkRequestBuilder<SyncWorker>()
    .setConstraints(constraints)
    .setBackoffCriteria(BackoffPolicy.EXPONENTIAL, 10, TimeUnit.SECONDS)
    .build()
```

---

### 4. Paginated Cache Boundary (RemoteMediator)

Implement Paging 3 `RemoteMediator` to load paginated payloads directly into local SQLite storage.

```kotlin
@OptIn(ExperimentalPagingApi::class)
class ItemRemoteMediator(
    private val db: AppDatabase,
    private val api: KtorClient
) : RemoteMediator<Int, ItemEntity>() {
    override suspend fun load(loadType: LoadType, state: PagingState<Int, ItemEntity>): MediatorResult {
        val page = when (loadType) {
            LoadType.REFRESH -> 1
            LoadType.PREPEND -> return MediatorResult.Success(endOfPaginationReached = true)
            LoadType.APPEND -> {
                val lastItem = state.lastItemOrNull() ?: return MediatorResult.Success(true)
                lastItem.pageIndex + 1
            }
        }
        return try {
            val response = api.getItemsList(page = page, limit = state.config.pageSize)
            db.withTransaction {
                if (loadType == LoadType.REFRESH) db.itemsDao().clearAll()
                db.itemsDao().insertAll(response.map { it.toEntity(pageIndex = page) })
            }
            MediatorResult.Success(endOfPaginationReached = response.isEmpty())
        } catch (e: Exception) { MediatorResult.Error(e) }
    }
}
```

---

### 5. Modular Dependency Injection Scopes

Feature modules must contain isolated scopes, relying on parent modules for core singletons.

```kotlin
// Core Network Module (Singleton scope)
val coreNetworkModule = module {
    single { OkHttp.create() }
    single { KtorClientFactory(get()).create() }
}

// Feature Profile Module (ViewModel Scope)
val featureProfileModule = module {
    viewModel { ProfileViewModel(get()) }
    factory { ProfileRepository(get()) }
}
```

---

### 6. Local Encryption & SSL Pinning

```kotlin
// Room SQLCipher Database encryption helper
val passphrase = SQLiteDatabase.getBytes("secure_passphrase".toCharArray())
val factory = SupportOpenHelperFactory(passphrase)
val db = Room.databaseBuilder(context, AppDatabase::class.java, "secure.db")
    .openHelperFactory(factory)
    .build()

// OkHttp SHA-256 Certificate Pinning
val pinner = CertificatePinner.Builder()
    .add("api.domain.com", "sha256/k2v657Wb5087yWb9087ywb8...")
    .build()
val client = OkHttpClient.Builder().certificatePinner(pinner).build()
```

---

### 7. Hardware Trusted Execution Environment (TEE)

Generate cryptographic keys inside the device's secure hardware enclave, requiring user biometrics to access them.

```kotlin
val keyStore = KeyStore.getInstance("AndroidKeyStore").apply { load(null) }

if (!keyStore.containsAlias("SecureKeyAlias")) {
    val keyGenerator = KeyGenerator.getInstance(
        KeyProperties.KEY_ALGORITHM_AES, 
        "AndroidKeyStore"
    )
    val spec = KeyGenParameterSpec.Builder(
        "SecureKeyAlias",
        KeyProperties.PURPOSE_ENCRYPT or KeyProperties.PURPOSE_DECRYPT
    )
        .setBlockModes(KeyProperties.BLOCK_MODE_GCM)
        .setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_NONE)
        .setUserAuthenticationRequired(true)
        .setUserAuthenticationValidityDurationSeconds(-1)
        .setInvalidatedByBiometricEnrollment(true)
        .build()

    keyGenerator.init(spec)
    keyGenerator.generateKey()
}
```

---

### 8. Concurrency Limits & Exception Boundaries

```kotlin
// Safe SupervisorScope Boundary
val scope = CoroutineScope(IO + SupervisorJob())
scope.launch { throw Exception("Task A Failed") }
scope.launch { /* Executes successfully despite Task A failure */ }

// Thread-Safe TokenBucket Rate Limiter
class TokenBucket(
    private val max: Int,
    private val refillRate: Float
) {
    private val mutex = Mutex()
    private var tokens = max.toFloat()
    private var lastRefill = System.nanoTime()

    suspend fun consume(): Boolean = mutex.withLock {
        refill()
        if (tokens >= 1.0f) { tokens -= 1.0f; true }
        else false
    }
    private fun refill() {
        val now = System.nanoTime()
        val elapsed = (now - lastRefill) / 1e9f
        tokens = (tokens + elapsed * refillRate).coerceAtMost(max.toFloat())
        lastRefill = now
    }
}
```

---

## 📚 Level Up Your Development:
If you are looking for complete, step-by-step implementations, architectural sequence diagrams, and pre-configured template zip files, check out our premium guides:

* [👉 **Android System Design & Architecture Playbook (₹599)**](https://yogirana.gumroad.com/l/nnxopw) — 12 advanced architectural playbooks: interactive sequence flowcharts, Room entity/DAO bindings, Hilt modular wiring, database caching, and WorkManager sync configurations.
* [👉 **Android Performance Optimization & Profiling Playbook (₹699)**](https://yogirana.gumroad.com/l/fgscvl) — Memory leaks analysis, object pools, JIT/AOT profiling, stability outputs, release baseline profiles, and Systrace analytics.
