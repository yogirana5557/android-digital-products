# Question 194: What is SSL Pinning, and how is it implemented in OkHttp?

**Category:** Networking & Data Serialization (Retrofit, OkHttp)  
**Difficulty:** Senior

---

### Answer

**SSL Pinning** is a security mechanism that prevents Man-in-the-Middle (MITM) attacks by checking the server's public key certificate against a list of pinned certificates preloaded in the app. In OkHttp, this is implemented using the `CertificatePinner` class added to the `OkHttpClient` builder.```kotlin
val pinner = CertificatePinner.Builder()
    .add("example.com", "sha256/hash_value")
    .build()
val client = OkHttpClient.Builder().certificatePinner(pinner).build()
```

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
