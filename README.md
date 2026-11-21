<p align="center">
  <img src="res/mipmap-xxxhdpi/ic_launcher.png" alt="YS Calculator icon" width="128">
</p>

<h1 align="center">YS Calculator</h1>

<p align="center">
  <strong>A beautiful, polished calculator for Android.</strong><br>
  Samsung One UI styling. English only. No account, no ads, no tracking.
</p>

<p align="center">
  <a href="https://github.com/yeasin0423/YSCalculator/releases/latest"><img src="https://img.shields.io/github/v/release/yeasin0423/YSCalculator?style=flat-square" alt="Latest release"></a>
  <a href="https://github.com/yeasin0423/YSCalculator/actions/workflows/build.yml"><img src="https://github.com/yeasin0423/YSCalculator/actions/workflows/build.yml/badge.svg" alt="Build status"></a>
  <img src="https://img.shields.io/badge/Android-12%2B-3DDC84?style=flat-square&logo=android&logoColor=white" alt="Android 12+">
  <img src="https://img.shields.io/badge/Design-Samsung_One_UI-1428A0?style=flat-square" alt="Samsung One UI styling">
</p>

<p align="center">
  <a href="https://github.com/yeasin0423/YSCalculator/releases/latest"><img src="https://img.shields.io/badge/Download-Latest_release-2ea043?style=for-the-badge" alt="Download latest release"></a>
</p>

---

YS Calculator is a personal calculator app rebuilt around Samsung One UI design language.
It performs exact arithmetic with no floating-point errors, keeps history locally, and ships
with a clean light and dark theme. Nothing leaves the device.

## At a glance

| Property | Support |
| --- | --- |
| Android | 12+ (API 31) |
| Calculation | Exact arithmetic engine |
| Display | One-line and two-line modes |
| History | Expression history with re-evaluation |
| Design | Samsung One UI only |
| Languages | English only |
| Permissions | None beyond defaults |
| Artifact | Release APK built by CI |

## Features

| | |
| --- | --- |
| **One UI look** | AMOLED-friendly dark and light palettes, clean typography, comfortable spacing, smooth animations. |
| **Exact arithmetic** | Rational-number based engine; results are precise, never rounded unexpectedly. |
| **History** | Every expression is saved; tap any past result to re-use it. |
| **Modes** | Standard and advanced pads, one-line and two-line displays. |
| **Private by default** | No internet permission, no analytics, no crash reporting, no account. |

## Download

Signed builds are published on the [releases page](https://github.com/yeasin0423/YSCalculator/releases).

## Build from source

Requirements: JDK 17 or newer and the Android SDK (compile SDK 35).

```sh
./gradlew assembleRelease
```

The APK is written to `build/outputs/apk/release/`. To sign your own build, create a git-ignored
`keystore.properties` in the project root:

```properties
storeFile=/path/to/your-release-key.jks
storePassword=...
keyAlias=...
keyPassword=...
```

### Gradle in CI

There is one **manual** workflow (`workflow_dispatch`); a normal push does not start a build:

- **Build release APK** – the normal build. It uses the Gradle wrapper (`./gradlew`), which downloads
  Gradle from `https://services.gradle.org/` and verifies its SHA-256
  (`distributionSha256Sum` in `gradle/wrapper/gradle-wrapper.properties`).

The workflow builds the unsigned release APK, shows checksums, uploads it as an artifact, and creates
(or refreshes) a GitHub release with the APK attached. The maintainer signs it locally; the signing
key never leaves the maintainer's computer.

## Project layout

```text
src/com/calculator/app/   app shell, calculation engine, UI
res/                      strings, themes, launcher icons
gradle/wrapper/           Gradle wrapper
.github/workflows/        manual release builds
```

Development rules for this fork live in [AGENTS.md](AGENTS.md).

## Credits

- [LineageOS ExactCalculator](https://github.com/LineageOS/android_packages_apps_ExactCalculator) —
  the upstream project this fork is based on.
- Samsung One UI — the visual language the interface follows.

## Disclaimer

YS Calculator is an independent project and is not affiliated with, endorsed by or connected to Samsung.
The One UI name is only used to describe the visual style the design is inspired by.
