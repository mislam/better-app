# Better App

Native mobile starter with SwiftUI and Jetpack Compose.

> This repository is not a JavaScript app. The root [`package.json`](package.json) exists for Bun Git hooks and commitlint.

## Setup

[Bun](https://bun.sh) 1.4+ (see `packageManager` in [`package.json`](package.json)):

```sh
bun install
```

## Docs

| Doc                                          | Use                                  |
| -------------------------------------------- | ------------------------------------ |
| [`docs/engineering.md`](docs/engineering.md) | Contracts, layout, and OS pins       |
| [`docs/roadmap.md`](docs/roadmap.md)         | Active milestone                     |
| [`CHANGELOG.md`](CHANGELOG.md)               | Shipped milestones                   |
| [`AGENTS.md`](AGENTS.md)                     | Cursor and coding agent instructions |

## iOS

Team stays unset, so the build skips code signing.

```sh
xcrun swift-format lint --strict --recursive apps/ios
xcodebuild -project apps/ios/Acme.xcodeproj -scheme Acme -destination 'generic/platform=iOS' CODE_SIGNING_ALLOWED=NO build
```

## Android

```sh
apps/android/gradlew -p apps/android ktlintCheck
apps/android/gradlew -p apps/android assembleDebug
```
