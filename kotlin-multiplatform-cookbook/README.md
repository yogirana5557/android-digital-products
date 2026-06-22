# 🚀 Kotlin Multiplatform & Compose Multiplatform Cookbook (Free Sample & Checklist)

Welcome to the open-source sample repository and study checklist for the **Kotlin Multiplatform (KMP) & Compose Multiplatform: Premium Developer Cookbook**.

This handbook is designed for senior and lead Android software engineers seeking copy-pasteable, robust, and highly technical cross-platform solutions. It covers 10 advanced recipes including Gradle version catalogs, shared Ktor networking engines, local relational Room databases, Compose multiplatform UI scaling, Koin DI setups, Voyager navigation, expect/actual bindings, multithreading flow observers, local caching settings, and iOS framework signing.

---

## 🛍️ Get the Full Playbook (₹199 / ₹299)

Get the complete compiled, ad-free PDF eBook containing all 10 recipes, under-the-hood explanations, and the pre-configured starter project template code zip:
* [👉 **Buy the Cookbook on Gumroad (₹199 / ₹299)**](https://yogirana.gumroad.com/l/oeiqh)
  - **Standard Edition (₹199)**: Includes print-ready 38-Page Master Playbook + 10 individual topic handbooks.
  - **Premium Edition (₹299)**: Includes all PDFs + the complete, pre-configured KMP Starter Project code zip.

---

## 📋 Kotlin Multiplatform & Compose Multiplatform Checklist

Use this checklist to track your learning progress or build cross-platform architectures:

* [x] **Recipe 1**: KMP Monorepo Project Structure & Centralized Version Catalogs. *(Read Free Sample Below)*
* [ ] **Recipe 2**: Shared Ktor HTTP Client with Content Negotiation & JSON Serialization.
* [ ] **Recipe 3**: Local Database Persistence using Jetpack Room Multiplatform.
* [ ] **Recipe 4**: Shared UI with Compose Multiplatform & Cross-Platform Resource Management.
* [ ] **Recipe 5**: Dependency Injection in Shared KMP Modules with Koin.
* [ ] **Recipe 6**: Shared Stack Navigation and Component State Hoisting via Voyager.
* [ ] **Recipe 7**: expect/actual Platform-Specific Feature Binding (Battery status & hardware details).
* [ ] **Recipe 8**: Multiplatform Threading model and Shared Flow observation in Swift.
* [ ] **Recipe 9**: Multiplatform Local Preferences Caching using MultiplatformSettings.
* [ ] **Recipe 10**: iOS Swift Package Manager & CocoaPods Xcode Framework Integration.

---

## 📖 Free Chapter Sample: Recipe 1 (KMP Setup & Gradle Configurations)

### Question
How do you structure a production-grade Kotlin Multiplatform monorepo? Explain version catalogs and configuration modules.

### Answer
A production KMP monorepo is structured into a `shared` Kotlin module containing business and data logic, alongside native platform apps (Android App, iOS App) that consume it. This isolates platform-specific views while keeping the core logic unified.

To maintain dependency version consistency across the entire project, Gradle **Version Catalogs** (`gradle/libs.versions.toml`) are used to centralize all dependencies, versions, and plugins.

The directory layout of a KMP monorepo:
- `gradle/libs.versions.toml` (version catalog declaration)
- `build.gradle.kts` (root project gradle)
- `settings.gradle.kts` (includes shared and platform modules)
- `shared/` (the KMP shared business logic module)
  - `build.gradle.kts` (KMP configuration for JVM, iOS targets)
  - `src/commonMain/` (pure Kotlin logic, Ktor, Room, viewmodels)
  - `src/androidMain/` (Android-specific implementations, Room database driver)
  - `src/iosMain/` (iOS-specific implementations, keychain bindings)
- `androidApp/` (thin imperative Android UI or Compose app)
- `iosApp/` (thin iOS Swift UI application)

#### Version Catalog configuration (`gradle/libs.versions.toml`)
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
android-library = { id = "com.android.library", version.ref = "androidGradlePlugin" }
compose-multiplatform = { id = "org.jetbrains.compose", version.ref = "composeMultiplatform" }
kotlin-compose = { id = "org.jetbrains.kotlin.plugin.compose", version.ref = "kotlin" }
room = { id = "androidx.room", version.ref = "room" }
ksp = { id = "com.google.devtools.ksp", version.ref = "ksp" }
```

#### Shared module configuration (`shared/build.gradle.kts`)
```kotlin
plugins {
    alias(libs.plugins.kotlin.multiplatform)
    alias(libs.plugins.android.library)
    alias(libs.plugins.compose.multiplatform)
    alias(libs.plugins.kotlin.compose) // Kotlin Compose compiler plugin
}

kotlin {
    androidTarget {
        compilerOptions {
            jvmTarget.set(org.jetbrains.kotlin.gradle.dsl.JvmTarget.JVM_17)
        }
    }
    
    // Configures iOS compilation targets (Simulator & Real Device ARM64)
    listOf(
        iosX64(),
        iosArm64(),
        iosSimulatorArm64()
    ).forEach { iosTarget ->
        iosTarget.binaries.framework {
            baseName = "SharedFramework"
            isStatic = true
        }
    }
    
    sourceSets {
        commonMain.dependencies {
            implementation(libs.ktor.client.core)
            implementation(libs.koin.core)
            implementation(libs.room.runtime)
            implementation(libs.sqlite.bundled)
        }
        
        androidMain.dependencies {
            implementation(libs.ktor.client.okhttp)
        }
        
        iosMain.dependencies {
            implementation(libs.ktor.client.darwin)
        }
    }
}

android {
    namespace = "com.example.shared"
    compileSdk = 34
    defaultConfig {
        minSdk = 24
    }
}
```

#### Follow-up / Cross Questions
* **What is the difference between static and dynamic framework linkage in the KMP iOS configuration?**
  A static framework (`isStatic = true`) compiles the Kotlin code directly into the iOS application binary at build time. This reduces runtime dynamic lookup overhead and avoids dynamic library signing issues in iOS, but it can increase the size of the final iOS binary if multiple frameworks are static. Dynamic frameworks are resolved at launch time but can lead to larger loading overheads.
* **Why do we define target architectures like iosSimulatorArm64 instead of just ios()?**
  Xcode simulators on modern Apple Silicon Macs run natively on ARM64 processors. Thus, to run and debug the iOS app natively without translation overhead, the `iosSimulatorArm64` compile target is required in the gradle script. Older Intel-based simulators require `iosX64`, while physical Apple iPhones require `iosArm64`.

> **GOOGLE TIP**: In system design interviews, emphasize modularity. Separating UI frameworks entirely from the core logic ensures the Kotlin codebase is testable on the JVM, while keeping the UI natively performance-optimized via SwiftUI and Jetpack Compose.
