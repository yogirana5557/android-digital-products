# 📱 Android Coding Round Question Bank (Free Sample & Checklist)

Welcome to the open-source sample repository and study checklist for the **Android Coding Round Question Bank (2026 Edition)**.

Most "Android interview prep" material is either generic trivia (lifecycle callbacks, Compose basics) or a generic LeetCode course with "Android" slapped on the title. This question bank is different: 27 real DSA coding problems, each framed exactly the way an Android interviewer actually asks them — an LRU cache that's really about evicting bitmap thumbnails, a sliding window that's really about debouncing a search bar, a graph cycle check that's really about Gradle module dependencies — with full Kotlin-idiomatic solutions, Big-O analysis, and the realistic follow-up question interviewers ask next.

---

## 🛍️ Get the Full Question Bank (₹499)
If you find this checklist and sample helpful, you can purchase the complete compiled, ad-free PDF containing all 27 problems, worked Kotlin solutions, and follow-up questions:
* [👉 **Buy the PDF on Gumroad (₹499)**](https://yogirana.gumroad.com/l/android-coding-round-question-bank) *(Includes print-ready PDF and lifetime updates)*

---

## 📋 The 27-Problem Checklist

Use this checklist to track your prep before a coding-round Android interview:

### 🔢 Chapter 1: Arrays & Strings Through an Android Lens
* [ ] **Topic 1**: Dedup a Scroll-Position-Triggered Analytics Event Stream
* [ ] **Topic 2**: Longest Run of Cache-Hit Thumbnails in a Scrolling Feed
* [ ] **Topic 3**: Merge Two Sorted Paginated Result Pages Without Duplicates
* [ ] **Topic 4**: Rotate a Carousel's Item Order by K Without Extra Storage

### 🗃️ Chapter 2: Hashing & Caching Patterns
* [ ] **Topic 5**: Build an LRU Cache for Decoded Bitmap Thumbnails
* [ ] **Topic 6**: Group Crash Reports by Normalized Stack Trace Signature
* [ ] **Topic 7**: First Non-Repeating Character in a Search-Bar Query (Streaming)
* [ ] **Topic 8**: Detect Duplicate Network Requests In-Flight (Request Coalescing)

### 🌳 Chapter 3: Trees, Tries & Search
* [ ] **Topic 9**: Autocomplete for a Search Bar Using a Trie
* [ ] **Topic 10**: Validate Balanced Brackets in a Deep-Link URL Template
* [ ] **Topic 11**: Lowest Common Ancestor in a Fragment Back-Stack Tree
* [ ] **Topic 12**: Serialize and Restore a Nested Preferences/Settings Tree

### ⚙️ Chapter 4: Concurrency & Coroutines Coding Rounds
* [ ] **Topic 13**: Implement a Suspend-Based Semaphore to Cap Parallel Image Downloads
* [x] **Topic 14**: Debounce a Search API Call Without Dropping the Latest Keystroke *(Read Free Sample Below)*
* [ ] **Topic 15**: Build a Suspend-Friendly Retry-With-Exponential-Backoff Wrapper
* [ ] **Topic 16**: Detect a Deadlock-Prone Lock Ordering Across Two Repositories

### 🪟 Chapter 5: Sliding Window & Rate Limiting
* [ ] **Topic 17**: Rate-Limit Retry Attempts to N Per Rolling 60-Second Window
* [ ] **Topic 18**: Longest Substring Without Repeating Characters, Applied to a Tag Parser
* [ ] **Topic 19**: Minimum Window Containing All Required Permission Strings
* [ ] **Topic 20**: Sliding-Window Maximum for a Rolling Average FPS Overlay

### 🕸️ Chapter 6: Graphs & Scheduling
* [ ] **Topic 21**: Topologically Sort Gradle Module Build Order
* [ ] **Topic 22**: Shortest Navigation Path Through a Deep-Link Graph
* [ ] **Topic 23**: Detect a Circular Inject/Provides Dependency in a DI Graph
* [ ] **Topic 24**: Minimum Number of Background Sync Workers to Cover All Dependent Jobs

### ⛰️ Chapter 7: Heaps & Top-K Problems
* [ ] **Topic 25**: Top-K Battery-Draining Background Processes
* [ ] **Topic 26**: K Closest Cached Locations to the User's Current Position
* [ ] **Topic 27**: Median Frame Time Over a Live Rolling Window

---

## 📖 Free Sample: Topic 14 (Debounce a Search API Call Without Dropping the Latest Keystroke)

### The Question
"As the user types into a search bar, only fire the network search after they pause for 300ms — but the *last* keystroke's query must always eventually fire, even if the user keeps typing right up until they stop. Implement this."

### Why Android Interviewers Ask This
It looks like a two-line `Flow` operator call, but the actual signal is whether the candidate understands *why* `collectLatest` (not `collect`) matters here: a slow network response for an old, superseded query must never be allowed to overwrite the UI with stale results. Candidates who reach for `collect` instead of `collectLatest` pass the happy path and fail the very next question.

### Solution
```kotlin
fun CoroutineScope.debouncedSearch(
    queries: Flow<String>,
    delayMs: Long = 300,
    onSearch: suspend (String) -> Unit
) {
    launch {
        queries
            .debounce(delayMs)
            .distinctUntilChanged()
            .collectLatest { query -> onSearch(query) }
    }
}
```

### Complexity
O(1) per emitted query. The important detail isn't asymptotic — it's that `collectLatest` cancels an in-flight `onSearch` call the moment a new (post-debounce) query arrives, so an old, slow response can never race ahead of a newer one and clobber the UI.

### Follow-Up Probe
> Expect: "Implement `debounce` yourself without the Flow operator, using `Channel` and `select`/delay-based cancellation."

This is a strong-signal follow-up that separates candidates who know *what* debounce does from those who understand *how* it's built on structured-concurrency cancellation — the full question bank covers the hand-rolled version alongside 26 other problems like it, spanning arrays, hashing, tries, concurrency, sliding windows, graphs, and heaps, all framed the same way: a real Android scenario first, the DSA underneath it second.

---

## 🧪 Get the Full Question Bank
Access all **27 problems across 7 chapters** — arrays/strings, hashing & caching, tries & trees, concurrency & coroutines, sliding window & rate limiting, graphs & scheduling, and heaps & top-k — complete with Kotlin solutions, Big-O analysis, and realistic follow-up questions:
* [👉 **Buy the PDF on Gumroad (₹499)**](https://yogirana.gumroad.com/l/android-coding-round-question-bank)
