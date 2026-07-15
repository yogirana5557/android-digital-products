# Android Gradle Build Speed & Centralized build-logic Playbook

Duplicated build configurations and unaligned dependency versions cause build slow-downs and configuration drift across modular projects. This playbook compiles production-grade setups to optimize compilation times and centralize build architecture using precompiled Kotlin DSL convention plugins.

---

## 🛠️ Centralized Config Quick Start

### 1. High-Impact Properties
Apply these properties in your root `gradle.properties` file to maximize parallel compilation and caching:

```properties
# Enable parallel module compilation
org.gradle.parallel=true

# Cache task inputs and reuse outputs
org.gradle.caching=true

# Reuse task configuration models
org.gradle.configuration-cache=true

# Allocate heap space and G1 Garbage Collector
org.gradle.jvmargs=-Xmx4g -XX:+UseG1GC -XX:MaxGCPauseMillis=200
```

### 2. Centralized Convention Plugin Layout
Centralize common dependency blocks using a composite `build-logic` directory:

```kotlin
// build-logic/convention/src/main/kotlin/android.library.gradle.kts
plugins {
    id("com.android.library")
    id("org.jetbrains.kotlin.android")
}

android {
    compileSdk = 34
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_17
        targetCompatibility = JavaVersion.VERSION_17
    }
}
```

---

## 📂 Download the Full Playbook (Free PDF)

This setup is part of the **AndroidDev Suite** resources. If you want the complete, print-ready 15-page A4 vector playbook (which includes KSP compiler transitions, build diagnostics scans, composite configurations, and task avoidance guidelines), download the PDF below:

➡️ **[Download the Free Playbook on Gumroad](https://yogirana.gumroad.com/l/gradle-optimization-cheatsheet)**

*The open-source code and sample configurations are free to browse on GitHub: [android-digital-products](https://github.com/yogirana5557/android-digital-products).*
