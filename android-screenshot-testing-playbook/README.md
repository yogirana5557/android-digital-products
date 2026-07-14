# Modern Android Screenshot Testing Playbook (Paparazzi & Roborazzi)

Running UI regression tests on a local JVM is 100x faster than running instrumentation tests on emulators. This guide shows how to write fast visual assertions in Jetpack Compose using Cash App's **Paparazzi** and **Roborazzi**.

---

## 🛠️ Implementation Quick Start

### 1. Gradle Configurations
Apply the plugins in your module-level build files:

```kotlin
// build.gradle.kts
plugins {
    id("app.cash.paparazzi") version "1.3.4"
    id("io.github.takahirom.roborazzi") version "1.12.0"
}
```

### 2. Writing a Paparazzi Test (Layout Rendering)
Paparazzi compiles and renders layouts in under 100ms using the Android Studio Layout Editor engine:

```kotlin
import app.cash.paparazzi.DeviceConfig
import app.cash.paparazzi.Paparazzi
import org.junit.Rule
import org.junit.Test

class CustomWidgetTest {

    @get:Rule
    val paparazzi = Paparazzi(
        deviceConfig = DeviceConfig.PIXEL_8,
        theme = "android:Theme.Material.Light.NoActionBar"
    )

    @Test
    fun verifyCardLayout() {
        paparazzi.snapshot {
            CustomProductCard(
                title = "Modern Screenshot Testing",
                price = "₹199"
            )
        }
    }
}
```

### 3. Writing a Roborazzi Test (UI Interactions)
Use Roborazzi paired with Robolectric to click view elements and capture intermediate UI states:

```kotlin
import androidx.compose.ui.test.junit4.createAndroidComposeRule
import androidx.compose.ui.test.onNodeWithText
import androidx.compose.ui.test.performClick
import com.github.takahirom.roborazzi.captureRoboImage
import org.junit.Rule
import org.junit.Test

@RunWith(RobolectricTestRunner::class)
class ExpandableCardTest {

    @get:Rule
    val composeTestRule = createAndroidComposeRule<MainActivity>()

    @Test
    fun testExpansionSnapshot() {
        composeTestRule.setContent { ExpandableCard() }
        
        // Capture initial
        captureRoboImage("card_closed.png")
        
        // Click
        composeTestRule.onNodeWithText("Details").performClick()
        
        // Capture expanded
        captureRoboImage("card_expanded.png")
    }
}
```

---

## 📂 Download the Full Playbook & Code Templates

This guide is part of the **AndroidDev Suite** premium handbooks. If you want the complete, print-ready 12-page vector PDF guide (which covers Google Compose Preview Screenshot Testing, version collisions in Kotlin 2.x, and custom font rendering rules) and the ready-to-run Android Studio project with pre-configured gradle plugins and a GitHub Actions workflow, check out the package below:

### 🛍️ Get the Playbook & Starter Code:
* **Tier 1: Playbook PDF Only** (₹199 / ~$2.49 USD) ➡️ **[Get PDF Playbook](https://yogirana.gumroad.com/l/screenshot-testing-playbook)**
* **Tier 2: Premium Developer Bundle** (₹399 / ~$4.99 USD) ➡️ **[Get PDF + Android Studio Starter Project + CI Workflows](https://yogirana.gumroad.com/l/screenshot-testing-playbook)**

*The open-source code and sample recipes are free to browse on GitHub: [android-digital-products](https://github.com/yogirana5557/android-digital-products).*
