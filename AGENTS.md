# AGENTS.md for YS Calculator

## Repo overview
- This is a personal calculator app based on LineageOS ExactCalculator source, now rebranded as YS Calculator with Samsung One UI-inspired design.
- The actual workspace is /home/yeasin/calculator-project/YSCalculator.
- Everything lives in a single package: src/com/calculator/app/ (main entry points, all logic, UI, tests, etc.).

## Developer workflow / CI constraints (do not ignore)
- **Build environment**: GitHub Actions `workflow_dispatch` build only (file: .github/workflows/build.yml). **NEVER** locally run Gradle, `gradlew`, build APK, use an emulator, or run ADB. If a CI build fails, share logs and fix together.
- **Git process**: All changes must be committed. You push your commits to GitHub. No local branch/P/R expectations unless discussed.
- **Single package**: `com.calculator.app` (namespace = applicationId). App name: `YS Calculator`, launcher name: `Calculator`. Current version: `2.1` (versionCode `21`).
- **Only one locale**: English-only. The present non-English `res/values-*` directories are upstream leftovers and will be pruned (discuss before changes).
- **No existing tests**: There's no test suite. Green CI is the only validation gate.

## Critical warnings
- **Never build locally**: No `./gradlew`, no local APK generation, no emulators, no ADB. All builds and testing must be done through the GitHub Actions workflow.
- **Never run ADB**: No ADB commands, no device communication, no manual testing outside CI.
- **CI is the only source of truth**: If something doesn't work in CI, we can't debug it unless we have the CI logs. Any issue without CI evidence cannot be validated.
- **No assumptions**: Never assume code works unless we have CI evidence. If something is unclear, ask me before making changes.

## High-signal commands and quirks
- Run the official build: nothing local; run `./gradlew assembleRelease` (or via CI).
- The CI workflow builds the unsigned release APK, shows checksums, uploads it as an artifact, and
  creates (or refreshes) a GitHub release with the APK attached. The maintainer signs it locally;
  the signing key never leaves the maintainer's computer.
- The only build artifact required by CI: `YS Calculator-unsigned-${{ github.ref_name }}` (path uses
  `build/outputs/apk/release/*.apk` wildcard to match AGP output).
- Third‑party libs location: `libs/com/hp/crcalc/1.0/crcalc-1.0.jar` (no mavenCentral). Don't touch this .jar.
- ProGuard: release build enables both code shrinking and resource shrinking; `proguard.flags` is the only rules file. Do not delete or rename this file.
- Theme setup: parent is `Theme.Material3Expressive.DayNight`. Button style options live in themes.xml; you'll be customizing themes, styles, colors, dimens.
- App icon: adaptive icon (following YSGallery pattern). `icon.png` scaled to 92% canvas fill placed at all densities as `res/mipmap-{mdpi,hdpi,xhdpi,xxhdpi,xxxhdpi}/ic_launcher_foreground.png` and `ic_launcher.png` (pre-26 fallback). Background drawable `res/drawable/ic_launcher_background.xml` (solid color). Adaptive icon XML `res/mipmap-anydpi-v26/ic_launcher.xml` references both. Referenced from `AndroidManifest.xml` as `@mipmap/ic_launcher`. No white space around the icon — background color fills any gaps.
- Debug build: `applicationIdSuffix = ".dev"` (debug builds get `com.calculator.app.dev`).

## Version scheme (follow this for every release commit)
- versionCode maps directly to versionName: versionCode `21` = version `2.1`, versionCode `59` = version `5.9`, versionCode `105` = version `10.5`.
- Update both `versionCode` and `versionName` in `build.gradle.kts` in the **same commit**.
- Example: next after `2.1`/`21` → `2.2`/`22`, then `2.3`/`23`, etc.

## What to avoid before discussing
- Touching code or resources without understanding first. If something is unclear, ask me before implementing changes. I won't assume intent or spark ideas out of thin air.

## Next steps for you (pre-implementation)
- Let me know what you think of this layout.
- If there are resources, docs, or directories you want to clean up now (e.g., remove all but English `res/values-*`, delete unused workflow files), let's discuss removal or what’s needed.
- Need an image of One UI calculator UI? Just tell me to search and I’ll grab a reference when you want.

Let's build something beautiful! ❤️