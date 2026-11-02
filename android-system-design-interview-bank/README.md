# 📱 Android System Design Interview Question Bank (Free Sample & Checklist)

Welcome to the open-source sample repository and study checklist for the **Android System Design Interview Question Bank (2026 Edition)**.

Most "mobile system design" prep material is written generically enough to cover iOS and Android with the same shallow pass, or costs $30–$200+ for a course bundle. This question bank is Android/Kotlin-specific: 30 real "design X" interview prompts with worked answers — why interviewers ask each one, how to structure a strong answer, a working Kotlin code blueprint, and the trade-off analysis that separates a senior answer from a junior one.

---

## 🛍️ Get the Full Question Bank (₹599)
If you find this checklist and sample helpful, you can purchase the complete compiled, ad-free PDF containing all 30 questions, code blueprints, and trade-off breakdowns:
* [👉 **Buy the PDF on Gumroad (₹599)**](https://yogirana.gumroad.com/l/android-system-design-interview-bank) *(Includes print-ready PDF and lifetime updates)*

---

## 📋 The 30-Question Checklist

Use this checklist to track your prep or shore up your system-design knowledge before a senior/staff Android interview:

### 🗂️ Chapter 1: Offline-First & Data Sync Architecture
* [x] **Topic 1**: Design an Offline-First Note-Taking App (like Google Keep) *(Read Free Sample Below)*
* [ ] **Topic 2**: Design a Robust Local-Remote Sync Engine with Conflict Resolution
* [ ] **Topic 3**: Design a "Single Source of Truth" Repository Layer
* [ ] **Topic 4**: Design Background Sync That Survives Process Death and Doze
* [ ] **Topic 5**: Design a Multi-Device Sync System (To-Do App Across Phone/Tablet/Web)

### 🖼️ Chapter 2: Caching, Image Loading & Network-Bound Resources
* [ ] **Topic 6**: Design an Image Loading & Caching Pipeline (like Instagram's Feed)
* [ ] **Topic 7**: Design the Network-Bound Resource Pattern for a Paginated Feed
* [ ] **Topic 8**: Design a Disk+Memory Two-Tier Cache for API Responses
* [ ] **Topic 9**: Design Cache Invalidation for a Content App (like a News Reader)
* [ ] **Topic 10**: Design Pre-fetching & Pagination for an Infinite Scroll Feed

### 🔌 Chapter 3: Real-Time & Streaming Systems on Android
* [ ] **Topic 11**: Design a Real-Time Chat App (WebSocket-Based)
* [ ] **Topic 12**: Design a Live Location-Sharing Feature (Find My Friends / Uber-Style Tracking)
* [ ] **Topic 13**: Design a Push Notification Delivery & De-duplication System
* [ ] **Topic 14**: Design a Real-Time Collaborative Editing Feature (Google Docs-Style, Mobile)
* [ ] **Topic 15**: Design a Live Metrics/Analytics Dashboard That Updates in Real Time

### 🏗️ Chapter 4: App Architecture at Scale
* [ ] **Topic 16**: Design a Multi-Module Architecture for a 50+ Engineer App
* [ ] **Topic 17**: Design the State Management Layer for a Complex Screen (Compose)
* [ ] **Topic 18**: Design a Navigation Architecture for a Deep-Linked, Multi-Flow App
* [ ] **Topic 19**: Design a Feature-Flagging & Remote-Config System for Gradual Rollouts
* [ ] **Topic 20**: Design a Dependency Injection Strategy for a Large Multi-Module App

### 📵 Chapter 5: Mobile-Specific Trade-offs & Constraints
* [ ] **Topic 21**: Design an App That Must Work Reliably on Low-End/Low-Memory Devices
* [ ] **Topic 22**: Design a Battery-Friendly Background Location Tracking Feature
* [ ] **Topic 23**: Design a Data-Usage-Conscious Sync Strategy for Metered Networks
* [ ] **Topic 24**: Design a Crash-Resilient, Session-Recoverable Checkout Flow
* [ ] **Topic 25**: Design Automatic Cache & Storage Cleanup When the Device Is Nearly Out of Space

### 🧩 Chapter 6: Full Mock System Design Walkthroughs
* [ ] **Topic 26**: Mock Walkthrough — Design Instagram's Mobile Feed
* [ ] **Topic 27**: Mock Walkthrough — Design a WhatsApp-Style Messaging App
* [ ] **Topic 28**: Mock Walkthrough — Design Dropbox-Style Mobile File Sync
* [ ] **Topic 29**: Mock Walkthrough — Design Uber-Style Live Driver Tracking
* [ ] **Topic 30**: Mock Walkthrough — Design Spotify-Style Offline Downloads

---

## 📖 Free Sample: Topic 1 (Design an Offline-First Note-Taking App)

### The Question
"Design the data layer for a note-taking app. Notes must be readable and editable with no network connection, and changes must sync to the server and other devices once connectivity returns."

### Why Interviewers Ask This
It's the simplest possible offline-first prompt, which is exactly why it's a good filter: candidates who haven't internalized "local database is the source of truth, not the network" reach for a network-first design and immediately paint themselves into a corner on the very first follow-up ("what happens if the user edits a note on a plane?").

### Strong Answer Walkthrough
- **Source of truth is the local database (Room), not the API.** Every read in the UI comes from a `Flow<List<Note>>` backed by Room. The network is an input to the local database, never something the UI waits on directly.
- **Writes are local-first, synced-later.** An edit commits to Room immediately (instant UI feedback) and is also recorded as a pending-sync mutation — either a `dirty` flag on the row, or a separate `PendingOperation` table if you need to preserve mutation order and support offline deletes.
- **A single sync worker owns the network.** A `SyncWorker` wakes on connectivity-regained and on a periodic schedule, pushes pending mutations, pulls remote changes, and reconciles.
- **Repository is the only thing that talks to both.** The ViewModel never touches Room or the API directly — it asks a `NoteRepository`, which hides whether data came from cache or network.

### Code Blueprint
```kotlin
@Entity
data class NoteEntity(
    @PrimaryKey val id: String,
    val title: String,
    val body: String,
    val updatedAt: Long,
    val dirty: Boolean = false,
    val deleted: Boolean = false
)

class NoteRepository(
    private val dao: NoteDao,
    private val api: NoteApi,
    private val workManager: WorkManager
) {
    fun observeNotes(): Flow<List<Note>> =
        dao.observeActive().map { entities -> entities.map { it.toDomain() } }

    suspend fun saveNote(note: Note) {
        dao.upsert(note.toEntity(dirty = true))
        enqueueSync()
    }

    suspend fun deleteNote(id: String) {
        dao.markDeleted(id, dirty = true)
        enqueueSync()
    }

    private fun enqueueSync() {
        val request = OneTimeWorkRequestBuilder<SyncWorker>()
            .setConstraints(Constraints.Builder().setRequiredNetworkType(NetworkType.CONNECTED).build())
            .build()
        workManager.enqueueUniqueWork("note-sync", ExistingWorkPolicy.KEEP, request)
    }
}
```

### Trade-offs & Follow-Up Probes
> Expect: "What if the same note is edited offline on two devices?" — that's Topic 2 (conflict resolution) in the full question bank, and naming it by name instead of hand-waving ("we'll just merge it") is what separates a senior answer here.

- Soft-delete (`deleted` flag, garbage-collected later) vs. hard-delete: soft-delete is almost always right offline, since a hard local delete can race a still-pending remote delete-mutation and resurrect a row on the next pull.
- A `dirty` boolean doesn't preserve *order* of mutations — fine for "last write wins" fields like a note body, insufficient for anything requiring causal ordering (a counter increment, a shared list's item order). Topic 2 covers the fix.

---

## 🧪 Get the Full Question Bank
Access all **30 questions across 6 chapters** — offline-first sync, caching, real-time systems, app architecture at scale, mobile-specific trade-offs, and 5 full mock walkthroughs — complete with Kotlin code blueprints and trade-off analysis:
* [👉 **Buy the PDF on Gumroad (₹599)**](https://yogirana.gumroad.com/l/android-system-design-interview-bank)
