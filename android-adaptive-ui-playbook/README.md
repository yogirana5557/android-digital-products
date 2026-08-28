# 📱 Jetpack Compose Adaptive UI & Foldables Playbook (Free Sample & Checklist)

Welcome to the open-source sample repository and study checklist for the **Jetpack Compose Adaptive UI & Foldables Playbook: Senior & Lead Engineer's Guide to Phones, Tablets, Foldables & Desktop Windows**.

Large-screen and foldable users spend meaningfully more than phone-only users, and Google Play now grants a visible "Optimized for large screens" badge to apps that meet the bar. Most teams still respond by stretching a phone layout wider — this handbook is the production-code playbook for actually building adaptive UI, not another blog post explaining `WindowSizeClass`. Every topic follows the same structure: the problem you hit building this, the fix, a complete code blueprint, and an under-the-hood explanation of *why* it works.

---

## 🛍️ Get the Full Playbook (₹699)
If you find this checklist and sample helpful, you can purchase the complete compiled, ad-free PDF eBook containing all 12 topics, code blueprints, and architectural breakdowns:
* [👉 **Buy the PDF Playbook on Gumroad (₹699)**](https://yogirana.gumroad.com/l/android-adaptive-ui-playbook) *(Includes print-ready PDF and lifetime updates)*

---

## 📋 The 12-Topic Adaptive UI Checklist

Use this checklist to track your learning progress or shore up your large-screen/foldable knowledge before a senior engineering interview:

### 🧱 Chapter 1: Foundations
* [x] **Topic 1**: WindowSizeClass & Breakpoints *(Read Free Sample Below)*
* [ ] **Topic 2**: Canonical Layouts: List-Detail, Supporting Pane & Feed
* [ ] **Topic 3**: One Layout, Not One Layout Per Form Factor

### 📐 Chapter 2: Foldables & Postures
* [ ] **Topic 4**: Detecting Folds & Hinges with Jetpack WindowManager
* [ ] **Topic 5**: Keeping Content Out of the Fold
* [ ] **Topic 6**: Table-Top & Book Posture Handling

### 🧩 Chapter 3: New Compose APIs
* [ ] **Topic 7**: Adaptive Navigation with NavigationSuiteScaffold
* [ ] **Topic 8**: Reacting to Environment Signals: The New MediaQuery API
* [ ] **Topic 9**: CSS-Inspired Grid & FlexBox Layouts in Compose

### 🚀 Chapter 4: Shipping It
* [ ] **Topic 10**: Desktop Windowing & Multi-Window
* [ ] **Topic 11**: Predictive Back Across Window Sizes
* [ ] **Topic 12**: Testing Adaptive Layouts & Meeting the Play Console Checklist

---

## 📖 Free Chapter Sample: Topic 1 (WindowSizeClass & Breakpoints)

### The Adaptive UI Challenge
The fastest way to "support tablets" is to take a phone layout and let it stretch — a single column of content centered in a sea of whitespace, or a list screen with no detail pane even though there's room for one. It compiles, it doesn't crash, and it fails a large-screen review instantly. The root cause is almost always hardcoded pixel or dp checks (`if (screenWidth > 600) ...`) sprinkled through the codebase instead of one deliberate, device-independent decision point.

### The Solution
Use `WindowSizeClass` to bucket the available width and height into `COMPACT`, `MEDIUM`, and `EXPANDED`, and branch layout decisions on the bucket, not the raw dp value. Compute it once, near the root of the screen, and pass it down — don't recompute it in every child composable.

### Production-Grade Code Blueprint
```kotlin
@Composable
fun ProductListingRoute() {
    val windowSizeClass = currentWindowAdaptiveInfo().windowSizeClass

    ProductListingScreen(
        widthSizeClass = windowSizeClass.windowWidthSizeClass,
    )
}

@Composable
fun ProductListingScreen(widthSizeClass: WindowWidthSizeClass) {
    when (widthSizeClass) {
        WindowWidthSizeClass.COMPACT -> {
            // Single column, one screen at a time. Phones in portrait.
            ProductListSingleColumn()
        }
        WindowWidthSizeClass.MEDIUM -> {
            // Two-up grid, still single-pane navigation. Small tablets,
            // large phones in landscape, unfolded book-style foldables.
            ProductGridTwoColumn()
        }
        WindowWidthSizeClass.EXPANDED -> {
            // Room for list + detail simultaneously. Tablets, desktop
            // windows, unfolded large foldables.
            ProductListDetailPane()
        }
        else -> ProductListSingleColumn()
    }
}
```

### Under-The-Hood Architectural Analysis
1. **Buckets, not breakpoints, are the actual API contract.** `COMPACT` is roughly under 600dp of width, `MEDIUM` roughly 600–840dp, `EXPANDED` above 840dp — but the exact numbers matter less than the fact that you're branching on Google's own device-independent classification, which gets refined over time. Code that branches on the bucket keeps working as the underlying thresholds get tuned; code that branches on a hardcoded `840` doesn't.
2. **Compute it once, at the routing layer.** `currentWindowAdaptiveInfo()` is cheap but not free, and more importantly, computing it in multiple places invites two child composables disagreeing about which layout mode they're in during a resize. Treat the size class the same way you'd treat a `NavController` — resolved once near the root, passed down explicitly.
3. **Height size class exists too, and gets ignored too often.** A `WindowHeightSizeClass` follows the same three-bucket model and matters for anything that reflows vertically — a bottom sheet, a two-row toolbar, a video player with controls beneath it. Large-screen review specifically checks landscape and split-screen configurations where height, not just width, is constrained.
4. **This replaces `sw600dp` resource qualifiers, not supplements them.** Teams migrating from the View system often keep both systems running — legacy layout-`sw600dp` XML *and* new Compose size-class branching — which reintroduces exactly the two-sources-of-truth drift this API exists to remove. Once a screen is on Compose, `WindowSizeClass` should be the only place responsive decisions get made.

---

## 🧪 Get the Full Playbook
Access all **12 adaptive UI topics** across foundations, foldables, new Compose APIs, and shipping concerns, complete with production-grade code blueprints and under-the-hood analysis:
* [👉 **Buy the PDF Playbook on Gumroad (₹699)**](https://yogirana.gumroad.com/l/android-adaptive-ui-playbook)
