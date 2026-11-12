# Changelog

**M#** = engineering milestone ([`docs/roadmap.md`](docs/roadmap.md)).

## Shipped

### M5 — chore: add commit hooks

- Add Bun git hooks that check commit messages with commitlint
- Format markdown with Prettier on commit
- Ignore `node_modules`

### M4 — feat(android): add app

- Add the Jetpack Compose Android app with an empty root view
- Check with ktlint and build the debug apk
- Ignore local Gradle files and recommend the Kotlin extension

### M3 — feat(ios): add app

- Add the SwiftUI iOS app with an empty root view
- Lint with swift-format and build for generic iOS
- Ignore local Xcode data and recommend the Swift extension

### M2 — docs: add agent and engineering scaffolding

- Add agent instructions for scope, git, and commit messages
- Record starter contracts, layout, and OS pins
- Index those docs from the README

### M1 — chore: init better-app repository

- Add the README and MIT license
- Add the starter roadmap with **Now** at **M2**
- Set line endings to LF and ignore `.DS_Store`
