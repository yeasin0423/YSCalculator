<p align="center">
  <img src="res/mipmap-anydpi/ic_launcher.xml" alt="YS Calculator Icon" width="120" height="120" />
  <br />
  <b>YS Calculator</b>
  <br />
  <sub>A beautiful, polished calculator app with Samsung One UI-inspired design</sub>
</p>

---

<p align="center">
  <b>Light theme</b> • <b>Dark theme</b> • <b>Clean UI</b> • <b>Smooth animations</b> • <b>English only</b>
</p>

---

## 📱 About

YS Calculator is a personal Android calculator app built from the ground up with a focus on beauty, simplicity, and usability. Inspired by Samsung's One UI design language, it features:

- ✨ **Clean, modern interface** — One UI-inspired buttons, typography, and spacing
- 🌗 **Light & dark themes** — Polished color schemes for both modes
- 🔢 **Exact arithmetic engine** — Precise calculations with no floating-point errors
- 🎨 **Beautiful animations** — Smooth transitions and micro-interactions
- 🇬🇧 **English only** — Focused, uncluttered experience

## 🛠 Tech Stack

- **Language:** Java (calculation engine) + Kotlin (new UI code)
- **Build:** Gradle (AGP 8.7.1), Java 17
- **Min SDK:** 31 (Android 12)
- **Target SDK:** 35
- **Package:** `com.calculator.app`
- **CI:** GitHub Actions (workflow_dispatch, unsigned release APK)

## 🚀 Getting Started

This project is built and released exclusively through GitHub Actions. No local builds, emulators, or ADB are used.

### Build via GitHub Actions

1. Push your changes to the `master` branch
2. Go to the **Actions** tab in GitHub
3. Run the **"build"** workflow (`workflow_dispatch`)
4. Download the unsigned release APK artifact
5. Sign it locally with your keystore
6. Install and test on your device

### Version Scheme

Version code maps directly to version name:
- `versionCode 11` → `versionName 1.1`
- `versionCode 59` → `versionName 5.9`
- `versionCode 105` → `versionName 10.5`

Update both together in every release commit.

## 📂 Project Structure

```
YS Calculator/
├── src/com/calculator/app/     # App source code
│   ├── Evaluator.java          # Calculation engine (Java)
│   ├── UnifiedReal.java        # Exact arithmetic (Java)
│   ├── BoundedRational.java    # Rational numbers (Java)
│   ├── Calculator.java         # Main activity (UI)
│   └── ...                     # Other UI & logic classes
├── res/                        # Resources (layouts, drawables, values)
├── .github/workflows/build.yml # CI build pipeline
├── build.gradle.kts            # Gradle build config
├── proguard.flags              # ProGuard/R8 rules
└── README.md                   # This file
```

## 🎨 Design

YS Calculator follows a Samsung One UI-inspired aesthetic:

- **Bottom-anchored controls** for one-handed use
- **Generous touch targets** and comfortable spacing
- **Rounded corners** and soft shadows
- **Consistent typography** across light and dark themes
- **Smooth animations** for button presses and state changes

## 📄 License

This project is derived from LineageOS ExactCalculator (Apache-2.0) and is maintained as a personal project.

---

<p align="center">
  Made with ❤️ for beautiful calculation
</p>