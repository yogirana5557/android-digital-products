# 🛡️ Android Security, Hardening & Reverse Engineering Handbook (Free Sample & Checklist)

Welcome to the local sample repository and study checklist for the **Android Security, Hardening & Reverse Engineering Handbook (The Mobile Security Blueprint)**.

This handbook is designed for senior and lead Android software engineers who want to protect their apps against static analysis decompiling, dynamic memory injections, root-access compromises, and man-in-the-middle network proxy tapping.

---

## 🛍️ Get the Full Playbook (₹799 / ₹999)
If you find this checklist and sample helpful, you can purchase the complete compiled, ad-free PDF eBook containing all 20 topics, security diagrams, and code wrappers:
* [👉 **Buy the PDF Handbook on Gumroad (₹799 Launch Deal)**](https://yogirana.gumroad.com/l/lspvc) *(Includes print-ready PDF, vector flowcharts, and lifetime updates)*

---

## 📋 The 20-Topic Security Checklist

Use this checklist to track your learning progress or prepare for senior developer security and systems design interviews:

### 🔑 Chapter 1: Reverse Engineering & Cryptographic Anchors
* [ ] **Topic 1**: Static Analysis Defenses, Decompilation, and R8 Hardening
* [ ] **Topic 2**: Hardware-Backed Keystore Cryptography (TEE & StrongBox)
* [ ] **Topic 3**: Biometric CryptoObject Authentication Wrappers
* [ ] **Topic 4**: Compile-Time Native String XOR Encryption (C++ JNI)
* [ ] **Topic 5**: ECDH Key Agreement Protocol & Dynamic Session Keys

### 💾 Chapter 2: Secure Storage & Network Isolation
* [ ] **Topic 6**: Room SQLite Database Encryption with SQLCipher
* [ ] **Topic 7**: EncryptedSharedPreferences Token Storage
* [ ] **Topic 8**: Advanced OkHttp SSL Pinning and Certificate Pinning
* [ ] **Topic 9**: Scoped Storage & Google Tink Streaming AEAD File Encryption
* [ ] **Topic 10**: Cleartext Policy Restrictions & VPN / Proxy Detection

### ⚙️ Chapter 3: Runtime Protection & Dynamic Defenses
* [ ] **Topic 11**: Multi-Layered Root & Emulator Detection (Java & Native NDK)
* [ ] **Topic 12**: App Tampering & Package Signature Self-Verification
* [x] **Topic 13**: Frida Instrumentation & Runtime Hooking Detection *(Read Free Sample Below)*
* [ ] **Topic 14**: Native ptrace Anti-Debugging & TracerPid Scanning
* [ ] **Topic 15**: Virtual Sandbox & Parallel Space Cloner Detection

### 🏗️ Chapter 4: Device Integrity & Server-Side Attestation
* [ ] **Topic 16**: Google Play Integrity API Token Attestation
* [ ] **Topic 17**: Server-Side Token Verdict Parsing & Device Profiles
* [ ] **Topic 18**: Anti-Replay Attack Protection & Nonces
* [ ] **Topic 19**: Google Play Integrity App Licensing Validation
* [ ] **Topic 20**: Device Security Attestation Fallbacks (SafetyNet & Hardware-Key Chains)

---

## 📖 Free Chapter Sample: Topic 13 (Frida Instrumentation & Runtime Hooking Detection)

### The Security Threat
Dynamic instrumentation frameworks like **Frida** allow hackers to inspect application memory, hook methods, and intercept class initializations at runtime. The attacking JavaScript/C++ code is injected directly into process memory without modifying the on-disk binary, completely bypassing static analysis protections and signature self-checks.

### The Hardening Defense
Monitor process status continuously from both Java and native C++ layers. Parse `/proc/self/maps` to identify injected dynamic library paths (e.g. `frida-agent.so`), scan local loopback ports for Frida's default listener (port `27042`), and monitor active threads for common naming patterns (like `gmain` or `gum-js-loop`).

### Production-Grade Code Blueprint
```kotlin
// Process Memory Maps monitoring for injected dynamic modules
class FridaHookDetector {
    
    fun isFridaInjected(): Boolean {
        return checkMemoryMaps() || checkFridaDefaultPort() || checkFridaThreads()
    }

    private fun checkMemoryMaps(): Boolean {
        try {
            val file = File("/proc/self/maps")
            val reader = BufferedReader(FileReader(file))
            var line: String?
            while (reader.readLine().also { line = it } != null) {
                val currentLine = line ?: continue
                // Look for common dynamic instrumentation agent naming conventions
                if (currentLine.contains("frida") || currentLine.contains("gum-js") || currentLine.contains("xposed")) {
                    reader.close()
                    return true
                }
            }
            reader.close()
        } catch (e: Exception) {
            // Handle parsing exceptions
        }
        return false
    }

    private fun checkFridaDefaultPort(): Boolean {
        // Frida server listens on port 27042 by default
        return try {
            val socket = Socket("127.0.0.1", 27042)
            socket.close()
            true // Connection successful, Frida is running!
        } catch (e: Exception) {
            false
        }
    }

    private fun checkFridaThreads(): Boolean {
        // Frida injects threads named "gmain", "gum-js-loop", etc.
        val threadSet = Thread.getAllStackTraces().keys
        for (thread in threadSet) {
            val name = thread.name
            if (name.contains("gmain") || name.contains("gum-js-loop") || name.contains("frida")) {
                return true
            }
        }
        return false
    }
}
```

### Under-The-Hood Security Analysis
1. **The Mechanics of Frida Library Injections**: Frida attaches to target processes using Linux debugging APIs (`ptrace`). Once attached, it injects a dynamic library (`frida-agent.so`) into the process heap and redirects execution entry hooks. This results in the agent library path appearing in the process memory mapping file `/proc/self/maps`.
2. **Reading `/proc/self/maps`**: `/proc/self/maps` is a virtual file exposed by the Linux kernel. It maps the virtual memory space of the running process, detailing where shared libraries (`.so` files) are loaded. Checking this dynamically at runtime is a primary defense against memory-only instrumentation.
3. **Dynamic Port Scans**: Although Frida server defaults to port `27042`, hackers frequently configure the server to run on custom ports to bypass static checks. Local socket polling can detect active server listener responses across ports.
4. **JNI-Level ptrace Anti-Attachment**: In your native NDK layer, call `ptrace(PTRACE_TRACEME, 0, 1, 0)`. Because Linux permits only one debugger to attach to a process, self-debugging blocks Frida's `ptrace` injection sequence.

---

## ⚡ Get the Full Playbook
Access all **20 advanced security topics** complete with flowcharts, cryptographic blueprints, and attestation guides:
* [👉 **Buy the PDF Playbook on Gumroad (₹799 Launch Deal)**](https://yogirana.gumroad.com/l/lspvc)
