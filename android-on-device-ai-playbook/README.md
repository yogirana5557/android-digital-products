# Android On-Device AI: Gemini Nano & AI Edge SDK Playbook

Running large language models (LLMs) locally on-device utilizes hardware-backed NPUs to enable zero-cost inference, offline capability, and absolute data privacy. This guide covers direct implementation of on-device generative AI in modern Android applications.

---

## 🛠️ Core Integration Steps

### 1. SDK Dependency
Add the Google AI Edge SDK client dependency to your `build.gradle.kts` version catalog:

```kotlin
// build.gradle.kts
dependencies {
    implementation("com.google.ai.edge.aicore:aicore:0.0.1-exp01")
}
```

### 2. direct AICore Client Wrapper
Initialize the local client service and stream tokens as they compute on the hardware NPU:

```kotlin
import com.google.ai.edge.aicore.AICore
import com.google.ai.edge.aicore.GenerativeModel
import com.google.ai.edge.aicore.GenerationConfig
import kotlinx.coroutines.flow.Flow
import kotlinx.coroutines.flow.flow

class GeminiNanoClient(private val context: Context) {
    private var generativeModel: GenerativeModel? = null

    suspend fun initialize(): Boolean {
        return try {
            val aiCore = AICore.get(context)
            val config = GenerationConfig.builder()
                .setTemperature(0.2f)
                .setMaxOutputTokens(512)
                .build()

            generativeModel = aiCore.createGenerativeModel(
                modelName = "gemini-nano",
                generationConfig = config,
                systemInstruction = "You are a senior Android security auditor."
            )
            true
        } catch (e: Exception) {
            false
        }
    }

    fun generateContentStream(prompt: String): Flow<String> = flow {
        val model = generativeModel ?: throw IllegalStateException("Model not initialized")
        val responseStream = model.generateContentStream(prompt)
        for (chunk in responseStream) {
            emit(chunk.text)
        }
    }
}
```

---

## 💡 Fallback Strategy (The Repository Pattern)
Since Gemini Nano requires specialized flagship hardware (Tensor G3/G4, Snapdragon 8 Gen 3+), route requests to the cloud (Gemini Pro API) when local AICore initialization fails:

```kotlin
interface AssistantRepository {
    fun getResponseStream(prompt: String): Flow<String>
}

class HybridAssistantRepository(
    private val localClient: GeminiNanoClient,
    private val remoteClient: GeminiCloudClient
) : AssistantRepository {
    private var isLocalSupported: Boolean = false

    suspend fun setup() {
        isLocalSupported = localClient.initialize()
    }

    override fun getResponseStream(prompt: String): Flow<String> {
        return if (isLocalSupported) {
            localClient.generateContentStream(prompt)
        } else {
            remoteClient.generateContentStream(prompt)
        }
    }
}
```

---

## 📂 Download the Full Playbook & Code Templates

This setup is part of the **Android Dev Suite** resources. If you want the complete, print-ready vector PDF guide (which includes system configurations, memory parameters, token budgets, and the Android Studio starter project), you can grab the package below:

### 🛍️ Get the Playbook & Starter Code Project:
* **Tier 1: Playbook PDF Only** (₹249 / ~$2.99 USD) ➡️ **[Get PDF Playbook](https://yogirana.gumroad.com/l/android-ai-playbook)**
* **Tier 2: Premium Developer Bundle** (₹499 / ~$5.99 USD) ➡️ **[Get PDF + Android Studio Starter Project](https://yogirana.gumroad.com/l/android-ai-playbook)**
  *(Includes a clean, Hilt-injected, ready-to-run Android Studio project implementing on-device chat using AICore and AI Edge SDK).*
