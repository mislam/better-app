# Engineering

> **M#** = engineering milestone. Shipped: [`CHANGELOG.md`](../CHANGELOG.md). Active work: [`roadmap.md` — Now](roadmap.md#now).

What this repo is: [`README.md`](../README.md). Contracts live in this file only.

## Contracts

| Topic | Decision |
| --- | --- |
| Layout | `apps/ios/`, `apps/android/`, `docs/`, `.cursor/`. A product adds `shared/` and `tools/` when it has files for them |
| UI | SwiftUI on iOS, Jetpack Compose on Android. No shared UI toolkit. The starter apps have an empty root view and no screen copy |
| Local records | When a product adds them: [SwiftData](https://developer.apple.com/documentation/swiftdata) on iOS and [Room](https://developer.android.com/training/data-storage/room) on Android, after a feature spec. The starter does not add a store |
| Preferences | When a product adds them: SwiftUI `AppStorage` on iOS and [Jetpack DataStore](https://developer.android.com/topic/libraries/architecture/datastore) on Android, after a feature spec. The starter does not add them |
| Parity | Product behavior lives in `docs/features/*.md`. A change updates the spec and both apps in the same milestone, or **Now** names which platform is behind. The starter ships no feature spec |
| Shared | Non-UI only, when a product adds it: copy, JSON, fixtures. No Swift or Kotlin sources that both apps compile. The starter does not create `shared/` |
| Tools | Product build scripts, when a product adds them. Invoked from the app build, not on the device. The starter does not create `tools/` |
| Naming | Repo paths: lowercase kebab-case. Swift and Kotlin files follow each platform’s usual names |
| Commits | Conventional Commits + commitlint |
| Agents | `AGENTS.md` + `.cursor/rules/`. Agents do not run mutating git commands unless the user asks |
| Versions | Minimum OS and dependency pins live in `docs/engineering.md` only |
| Bundle id | `com.example.betterapp` on both platforms. Replace `com.example` before any store registration |
| Display name | Better App |
| Numbering | After this starter ships, app-developer milestones start at **M1** |

The layout below is the finished template.

```text
better-app/
  README.md
  AGENTS.md
  CHANGELOG.md
  docs/
    engineering.md
    roadmap.md
  apps/ios/
  apps/android/
  .cursor/rules/
  .github/workflows/
  package.json
```

`.gitignore` lists repo junk and, later, the paths a new tool writes. Do not commit large binaries, secrets, or local SDK drops; add those patterns with the change that introduces the files. `.cursorignore` is not a second copy of `.gitignore`.

## Versions

| Pin | Value | Source |
| --- | --- | --- |
| iOS deployment target | 27.0 | Xcode 27.2, [SDK and system requirements](https://developer.apple.com/xcode/system-requirements/) |
| Android `minSdk` | 26 | Android 8.0, set by this starter |
| Android `compileSdk` and `targetSdk` | 36 | Android 16, [App compatibility in Android](https://developer.android.com/guide/app-compatibility) |
