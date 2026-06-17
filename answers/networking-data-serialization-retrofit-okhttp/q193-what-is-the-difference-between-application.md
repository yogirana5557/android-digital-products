# Question 193: What is the difference between Application Interceptors and Network Interceptors in OkHttp?

**Category:** Networking & Data Serialization (Retrofit, OkHttp)  
**Difficulty:** Mid

---

### Answer

* **Application Interceptors**: Added via `addInterceptor()`. They run exactly once, even if the request is served from cache or retried due to connection failure. They observe the final request and response.
* **Network Interceptors**: Added via `addNetworkInterceptor()`. They run on the network layer, observing actual network transmissions (including redirects, retries, and headers). They do not run if the response is cached.

---
*This is a free sample answer from the **Android Interview Question Bank**. Access all 300+ questions, detailed code examples, and architectural system designs in the premium PDF handbook.*

[📥 Download the Full PDF eBook](https://yogirana.gumroad.com/l/ljzae)
