# Better App

Native mobile starter with SwiftUI and Jetpack Compose.

## Docs

| Doc | Use |
| --- | --- |
| [`docs/engineering.md`](docs/engineering.md) | Contracts, layout, and OS pins |
| [`docs/roadmap.md`](docs/roadmap.md) | Active milestone |
| [`CHANGELOG.md`](CHANGELOG.md) | Shipped milestones |
| [`AGENTS.md`](AGENTS.md) | Cursor and coding agent instructions |

## iOS

Team stays unset, so the build skips code signing.

```sh
xcrun swift-format lint --strict --recursive apps/ios
xcodebuild -project apps/ios/Acme.xcodeproj -scheme Acme -destination 'generic/platform=iOS' CODE_SIGNING_ALLOWED=NO build
```
