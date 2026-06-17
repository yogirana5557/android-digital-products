# Android System Design & Architecture Playbook

Welcome to the public resources folder for the **Android System Design & Architecture Playbook (Senior & Lead Engineer's Guide)**.

This folder contains a syllabus checklist of all 12 architectural playbooks, along with **2 complete free samples** directly exported from the premium print-ready playbook.

---

## 🛍️ Get the Full Playbook

The full Playbook is a premium, print-ready, ad-free PDF containing all 12 topics with vector sequence flowcharts, step-by-step data flows, comprehensive multi-file Kotlin blueprints (Hilt wring, Room entities, and unit testing scopes), and under-the-hood compilations of Gradle caching, SQLCipher page mapping, and TEE Keystore security.

👉 **[Get Instant Access on Gumroad](https://yogirana.gumroad.com/l/nnxopw)** (₹599 / $24.99)

---

## 📋 Table of Contents & Study Checklist

Use this checklist to track your learning progress:

- [ ] **Chapter 1: Multi-Module Architecture & Gradle**
  - [ ] **Topic 1**: Centralized Dependency Management with Version Catalogs (`libs.versions.toml` & Platform BOM)
  - [ ] **Topic 2**: Custom Gradle Convention Plugins for Modular Scaling (precompiled composite builds)
  - [ ] **Topic 3**: Modular Architecture Boundaries & Decoupling Patterns (feature-api vs feature-impl) *(FREE SAMPLE BELOW)*
- [ ] **Chapter 2: High-Performance Data Layers & Offline Sync**
  - [ ] **Topic 4**: Single Source of Truth (SSOT) with Network-Bound Resource (database query flow hooks)
  - [ ] **Topic 5**: Offline-First Synchronizer with Room & WorkManager (mutations queue + exponential backoff)
  - [ ] **Topic 6**: Pagination with Local Cache Boundary (RemoteMediator & RemoteKeys database indexing)
- [ ] **Chapter 3: Networking, Concurrency & Real-Time Sync**
  - [ ] **Topic 7**: OAuth2 Token Refresh Rotation (Thread-safe synchronized double-lock OkHttp Authenticator)
  - [ ] **Topic 8**: Real-Time Event Channels with WebSockets & Coroutines StateFlow (cold callbackFlow + lifecycle sharing)
  - [ ] **Topic 9**: Structured Concurrency & Job Coordination (Application-scoped SupervisorJob TEE context boundaries)
- [ ] **Chapter 4: Mobile Security & Enterprise Hardening**
  - [ ] **Topic 10**: SSL Certificate Pinning & Network Security Configurations (OkHttp CertificatePinner + native system-level XML trust)
  - [ ] **Topic 11**: Secure Local Caching with SQLCipher & EncryptedSharedPreferences (TEE key isolation + SQLite page encryption) *(FREE SAMPLE BELOW)*
  - [ ] **Topic 12**: Biometric Authentication with Cryptographic Keys (Hardware Keystore locked keys + CryptoObject Cipher validation)

---

## 🎁 Free Sample Playbooks

### Sample #1: Modular Architecture Boundaries & Decoupling Patterns (Topic #3)

#### The System Design Challenge
Splitting a project into modules without strict boundaries often creates circular dependencies, where module A references module B, and B references A. This breaks compiler caching, increases build times, and tightly couples features, preventing isolated testing. Additionally, leaking implementation details makes code fragile and hard to scale.

#### The Architectural Solution
Enforce a strict unidirectional dependency graph by structuring the codebase into feature implementation (`-impl`) and feature API (`-api`) modules. Features must never depend on other features directly. Instead, they communicate strictly via lightweight feature-api modules using interfaces and dependency injection.

#### Production-Grade Blueprint Code
```kotlin
// 1. :feature:details-api (Contract Definition Module)
interface DetailsFeatureLauncher {
    fun launch(context: Context, productId: String)
}

// 2. :feature:details-impl (Implementation Module)
class DetailsFeatureLauncherImpl @Inject constructor() : DetailsFeatureLauncher {
    override fun launch(context: Context, productId: String) {
        val intent = Intent(context, DetailsActivity::class.java).apply {
            putExtra("EXTRA_PRODUCT_ID", productId)
        }
        context.startActivity(intent)
    }
}

// 3. :feature:details-impl (Hilt Binding Declaration)
@Module
@InstallIn(SingletonComponent::class)
abstract class DetailsFeatureModule {
    @Binds
    abstract fun bindDetailsLauncher(
        impl: DetailsFeatureLauncherImpl
    ): DetailsFeatureLauncher
}

// 4. :feature:home (Depends only on details-api, not the details-impl module!)
@Composable
fun HomeScreen(detailsLauncher: DetailsFeatureLauncher) {
    val context = LocalContext.current
    Button(onClick = { detailsLauncher.launch(context, "102") }) {
        Text("Go to Product Details")
    }
}
```

#### Architectural Deep-Dive & Best Practices
- **Unidirectional Graph Decoupling**: Feature modules only import public `-api` contracts. The central app module depends on both `-impl` and `-api` modules, resolving the interface bindings at compile-time via Hilt, breaking circular dependencies.
- **Incremental Compilation Speedups**: Modifying Jetpack Compose layouts, logic, or resources inside `:feature:details-impl` does not trigger re-compilation of `:feature:home` because home's dependency on the static `-api` binary remains unchanged.
- **Strict Encapsulation**: Marking classes (ViewModels, Repositories, Entities) as `internal` within implementation modules guarantees that internal design decisions cannot be leaked, preserving architecture purity.
- **Standalone Module Running**: Because `-impl` modules are decoupled from other features, they can be easily compiled inside small, lightweight standalone launcher applications, reducing test-run iteration times from minutes to seconds.

---

### Sample #2: Secure Local Caching with SQLCipher & EncryptedSharedPreferences (Topic #11)

#### The System Design Challenge
Storing access tokens, personal details, or local database caches in standard Room databases or SharedPreferences allows rooted users or physical device thieves to read the SQLite files or XML preference sheets directly in plain text. Backing up the app allows plaintext database extraction, violating local security guidelines.

#### The Architectural Solution
Implement hardware-backed, encrypted storage: encrypt Room databases using the `SQLCipher` library, and secure key-value caches using Google's `EncryptedSharedPreferences` backed by Android's hardware keystore keys. All reads/writes perform transparent on-the-fly encryption.

#### Production-Grade Blueprint Code
```kotlin
// 1. EncryptedSharedPreferences Wrapper
class SecurePrefsManager(context: Context) {
    private val masterKey = MasterKey.Builder(context)
        .setKeyScheme(MasterKey.KeyScheme.AES256_GCM)
        .build()

    private val encryptedPrefs = EncryptedSharedPreferences.create(
        context, "secure_user_prefs", masterKey,
        EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
        EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
    )

    fun saveToken(token: String) = encryptedPrefs.edit().putString("jwt", token).apply()
    fun getToken(): String? = encryptedPrefs.getString("jwt", null)
}

// 2. SQLCipher Room Database factory configuration
@Module
@InstallIn(SingletonComponent::class)
object DatabaseModule {
    @Provides
    @Singleton
    fun provideDatabase(@ApplicationContext context: Context): SecureAppDatabase {
        val passPhrase = SQLiteDatabase.getBytes("secure_passphrase".toCharArray())
        val factory = SupportFactory(passPhrase)

        return Room.databaseBuilder(
            context, SecureAppDatabase::class.java, "secure-app-db"
        ).openHelperFactory(factory).build()
    }
}
```

#### Architectural Deep-Dive & Best Practices
- **Keystore Hardware Key Isolation**: `MasterKey` generates cryptographic keys inside the Android Keystore system. The key remains inside the hardware-backed security module (TEE or StrongBox) and is never exposed to the application software layer.
- **AES-256 Crypto Operations**: EncryptedSharedPreferences uses deterministic encryption (AES-256-SIV) for preference keys so they remain searchable, and authenticated encryption (AES-256-GCM) for preference values to prevent tampering.
- **SQLCipher SQLite Integration**: `SupportFactory` integrates SQLCipher directly with Room's database factory. SQLCipher performs real-time, block-level page encryption and decryption as data travels to and from disk.
- **Database Password Security**: Storing database passwords in plaintext in code defeats the purpose of SQLCipher. Passwords should be derived dynamically from Keystore-encrypted files or supplied by user credentials during session startup.

---

## 🛍️ Upgrade to the Full Guide Now

Get all 12 complete blueprints, sequence diagrams, and deep dives:

👉 **[Buy Android System Design & Architecture Playbook on Gumroad](https://yogirana.gumroad.com/l/nnxopw)**
