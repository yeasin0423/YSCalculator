# AGENTS.md for ExactCalculator (fork of LineageOS android_packages_apps_ExactCalculator)

## Repo overview
- This is a fork of LineageOS's ExactCalculator (android_packages_apps_ExactCalculator.git), aiming for a Samsung One UI-inspired design.
- The actual workspace is /home/yeasin/calculator-project/android_packages_apps_ExactCalculator.
- Everything lives in a single package: src/com/android/calculator2/ (main entry points, all logic, UI, tests, etc.).

## Developer workflow / CI constraints (do not ignore)
- **Build environment**: GitHub Actions `workflow_dispatch` build only (file: .github/workflows/build.yml). **NEVER** locally run Gradle, `gradlew`, build APK, use an emulator, or run ADB. If a CI build fails, share logs and fix together.
- **Git process**: All changes must be committed. You push your commits to GitHub. No local branch/P/R expectations unless discussed.
- **Single package**: `com.android.calculator2` (namespace = applicationId). This repo is the **only** buildable app; there's no multi-project structure.
- **Only one locale**: English-only. The present non-English `res/values-*` directories are upstream leftovers and will be pruned (discuss before changes).
- **No existing tests**: There's no test suite. Green CI is the only validation gate.

## Critical warnings
- **Never build locally**: No `./gradlew`, no local APK generation, no emulators, no ADB. All builds and testing must be done through the GitHub Actions workflow.
- **Never run ADB**: No ADB commands, no device communication, no manual testing outside CI.
- **CI is the only source of truth**: If something doesn't work in CI, we can't debug it unless we have the CI logs. Any issue without CI evidence cannot be validated.
- **No assumptions**: Never assume code works unless we have CI evidence. If something is unclear, ask me before making changes.

## High-signal commands and quirks
- Run the official build: nothing local; run `./gradlew assembleRelease` (or via CI) but be prepared to run `generateBp` after any Gradle dep change.
- The only build artifacts required by CI: `ExactCalculator-release.apk` (uploaded as artifact) and a clean `Android.bp` generated from the Gradle model.
- Non-obvious deps in the source code (search for imports): androidx.core.*, androidx.constraintlayout.motion.*, androidx.fragment.*, androidx.recyclerview.*, and third‑party `com.hp:crcalc:1.0` (unmanaged outside AOSP). Editing `build.gradle.kts` without adjusting `Android.bp` → immediate CI red.
- WebKit for Licenses: `assets/licenses.html` powers the Licenses screen via a WebView; ensure it stays in sync with actual license texts when you update any dependency.
- Theme setup: parent is `Theme.Material3Expressive.DayNight`. Button style options live in themes.xml; you’ll be customizing themes, styles, colors, dimens.
- Third‑party libs location: `libs/com/hp/crcalc/1.0/crcalc-1.0.jar` (no mavenCentral). Don't touch this .jar.
- ProGuard: release build enables both code shrinking and resource shrinking; `proguard.flags` is the only rules file. Do not delete or rename this file.
- Debug appId: `-dev` suffix? (appIdSuffix `.dev` per `build.gradle.kts`, so debug builds get `com.android.calculator2.dev`).
- Generated files: `Android.bp` is generated; it's committed and must stay generated from `build.gradle.kts` (targetSdk, minSdk, versionCode, versionName).

## What to avoid before discussing
- Removing upstream-typical directories (`.github/workflows/*`, `docs/*`, `assets/*`, non-English `res/values-*`) unless you are 100% sure they’re not needed for your design (e.g., any internal tools, translation infrastructure, LICENSE rendering, REUSE compliance).
- Touching code or resources without understanding first. If something is unclear, ask me before implementing changes. I won’t assume intent or spark ideas out of thin air.

## Next steps for you (pre-implementation)
- Let me know what you think of this layout.
- If there are resources, docs, or directories you want to clean up now (e.g., remove all but English `res/values-*`, delete unused workflow files), let's discuss removal or what’s needed.
- Need an image of One UI calculator UI? Just tell me to search and I’ll grab a reference when you want.

Let's build something beautiful! ❤️