# Roadmap

> **M#** = engineering milestone. Shipped work is recorded in [`CHANGELOG.md`](../CHANGELOG.md) once that file exists. This repo is the `mislam/better-app` native mobile starter; copy it for a new iOS and Android app.

**New chat:** implement the milestone under **Now** in this file. Do not start the next one.

This file is the build queue for the starter. A session with no other history does only **Now**.

## How to run a milestone

- Do only the milestone under **Now**. Do not implement **Upcoming** or **Later**.
- Do not invent product features, vendor SDKs, or an asset pipeline. See [Out of scope](#out-of-scope).
- Do not add ignore rules, commands, or config for a tool this milestone does not introduce. Put generated paths in `.gitignore`, using the paths that tool writes. Cursor already skips gitignored files, so do not copy those rules into `.cursorignore`. Add `.cursorignore` only for a file Cursor would still index.
- Contracts live in `docs/engineering.md`.
- Read `AGENTS.md` and `docs/engineering.md` with this file.
- **Already exists** on a card is the baseline. If the repo disagrees, trust the repo for work that is already done. Do not redo it and do not recreate this queue.
- Mark each acceptance box `[x]` when that item is done. Close-out is not a checkbox.
- One commit. Subject is the Conventional Commits subject on the milestone. One change: subject only. More than one change: a blank line, then `- ` bullets. Each bullet is an imperative sentence. Do not mention changelog entries or advancing **Now** in the commit body.
- Agents do not run mutating git commands unless the user asks for that command in the current message. Suggest the subject. The user commits.
- **Close-out**, in the same change, when every acceptance box under **Now** is `[x]`:
  1. Append that milestone to `CHANGELOG.md` under **Shipped** as `### M# — subject` (newest first). A few short bullets on what landed. Do not copy acceptance text, file contents, copyright lines, or instructions about what to skip. Create the changelog only if the milestone says to.
  2. Move the next **Upcoming** milestone into **Now** and delete the finished milestone from this file.
  3. Stop. Do not start the next milestone.
- **M1** creates `CHANGELOG.md` with only the **M1** shipped entry. That is the starter history, not an empty product changelog. **M2–M7** prepend their own entries. **M8** clears **Shipped** and replaces this file with an empty Now / Upcoming / Later page. Starter ids **M1–M8** then exist only in git history.
- If **Now** says there is no open milestone, the starter is finished. Do not invent a milestone.

## Out of scope

The template stops at two apps that build. It ships no screen. A product repo adds the rest. Document each addition in that repo’s `docs/engineering.md` and a `docs/features/*.md` file before code.

| Add in the product repo | Where it is recorded |
| --- | --- |
| Product screens and behavior | `docs/features/<name>.md`, then iOS and Android |
| On-device records and preferences | The SwiftData, Room, `AppStorage`, and DataStore choices in `docs/engineering.md`, then a feature spec, then both apps |
| A native library (SPM, Gradle, or a copied binary) | One pin (version or commit) in `docs/engineering.md`; both apps if both need it |
| Build scripts that fetch or package assets | `tools/`, invoked from the app build, not at runtime on the device |
| Large or generated assets | Gitignored; how to produce them is in `tools/` or engineering when the product adds them |
| Accounts, backend, sync, push, purchases | Their own feature docs |

If only one platform ships in a milestone, **Now** says so.

These better-saas pieces do not get a milestone here: auth secret, Postgres, email auth, Vercel, Svelte skills, and Svelte MCP. That is the web stack. Do not add them.

**M8** folds this boundary into `docs/engineering.md` and deletes this section.

## Now

### M3 — `feat(ios): add app`

**Already exists:** **M2** docs. No `apps/` yet. No root `package.json`, no CI, and no `.cursor/rules/`. Android is behind until **M4**. Do not add a feature spec or a note elsewhere.

The user creates the Xcode project once. The session does not drive the Xcode app. If that project is not on disk yet, stop and ask them to create it, then ask where they saved it. Do not hand-write a project and do not use XcodeGen, Tuist, or `swift package init`.

**Acceptance:**

- [ ] The user’s project is Xcode’s iOS App template ([Creating an Xcode project for an app](https://developer.apple.com/documentation/xcode/creating-an-xcode-project-for-an-app)): File > New > Project, iOS, App. Product Name `BetterApp`. Organization Identifier `com.example`. Interface SwiftUI. Language Swift. Storage None. Testing System None. Leave Team unset. They may save it anywhere. Move it under `apps/ios/` if it is not already there. Target and scheme `BetterApp`, display name **Better App**, bundle id `com.example.betterapp`. The root view is empty. Delete sample text the template inserts, including “Hello, world!”. Do not add a title, a platform line, or any other copy.
- [ ] Do not add a test target. There is no screen behavior to test.
- [ ] Wire an Apple `swift-format` lint check (not SwiftLint or another third-party formatter). Write the `swift-format` command and the `xcodebuild` build command in the README, including the project, scheme, and destination `generic/platform=iOS`. Build only. No test action and no simulator name.
- [ ] Append `.gitignore` rules for the user-specific Xcode data and build products this project writes. Commit the project, shared scheme, and sources. Do not add `.cursorignore` for these paths.
- [ ] Add `.vscode/extensions.json` recommending the official Swift extension (`swiftlang.swift-vscode`). If the marketplace id has changed, use the extension published by the Swift project and record that id.
- [ ] Record any new version pin (Xcode, Swift, iOS deployment target if it differs from engineering) in `docs/engineering.md` only.

**Non-goals:** no Android project, no feature spec, no third-party native SDK, no SPM packages beyond Apple’s SDKs, no root `package.json`, no CI workflow, no Cursor rules. Do not start **M4**.

**Close-out:** Prepend **M3** under **Shipped**. Move **M4** into **Now**. Delete this **M3** section.

## Upcoming

### M4 — `feat(android): add app`

**Already exists:** the iOS app and its README commands. No root `package.json`, no CI, and no `.cursor/rules/`. Do not rewrite the iOS app.

**Acceptance:**

- [ ] Add a Gradle project under `apps/android/` by running the official Android CLI. Do not open Android Studio. Use the empty Compose activity template ([`android create`](https://developer.android.com/tools/agents/android-cli/commands/create)). Install the CLI from [Download Android CLI](https://developer.android.com/tools/agents/android-cli/download) when it is missing. Do not commit the CLI, and do not run `android init` to vendor an agent skill. Run `android create --list` and use the empty Compose activity template (`empty-activity` in the current docs). Record the template name if that list uses another name for the same template. Create it with `--name="Better App"`, `--application-id=com.example.betterapp`, `--namespace=com.example.betterapp`, `--min-sdk=26`, and `--output=apps/android`. Jetpack Compose only, via the Android Gradle Plugin and AndroidX Compose. Do not add Room, DataStore, a Navigation library, or a ViewModel. The root view is empty. Delete sample text the template inserts. Do not add a title, a platform line, or any other copy. `minSdk`, `compileSdk`, and `targetSdk` match `docs/engineering.md`. If the template’s `compileSdk` or `targetSdk` differs, change them to those pins.
- [ ] Do not add a unit test. There is no screen behavior to test.
- [ ] Wire `ktlint` as a build-time check, not as a library shipped in the app. Use the Gradle wrapper (`./gradlew`) so **M6** does not install a separate Gradle. Write the wrapper tasks for `ktlint` and the debug build in the README. No test task.
- [ ] Append `.gitignore` rules for the local machine files and build outputs this project writes, including `local.properties`, `.gradle/`, module `build/` directories, and packaged apk/aab files. Commit the wrapper and project scripts. Do not add `.cursorignore` for these paths.
- [ ] Add the Kotlin language extension to `.vscode/extensions.json` (marketplace id `fwcd.kotlin` unless that id has moved; then use the current Kotlin language extension and record the id).
- [ ] Record Kotlin, Android Gradle Plugin, Compose, `ktlint`, and the Android CLI version in `docs/engineering.md` only.

**Non-goals:** no third-party native SDK besides AndroidX Compose and the build-time `ktlint` plugin. No feature spec, no root `package.json`, no CI workflow, no Cursor rules. Do not start **M5**.

**Close-out:** Prepend **M4** under **Shipped**. Move **M5** into **Now**. Delete this **M4** section.

### M5 — `chore: add commit hooks`

**Already exists:** both apps. The README lists their format and build commands. No root `package.json`. No `.cursor/rules/`. No `docs/features/`, `shared/`, or `tools/`. Do not create those paths.

Use **npm** and commit `package-lock.json`. Do not adopt Bun. This is not a JavaScript application.

**Acceptance:**

- [ ] Add a root `package.json` whose only job is Git hooks and commitlint. `private: true`. Dev dependencies only: `husky`, `@commitlint/cli`, `@commitlint/config-conventional`, `lint-staged`, and `prettier`. A `prepare` script installs Husky. No app dependencies, no ESLint, no test runner, no Vite.
- [ ] Add `commitlint.config.js` extending `@commitlint/config-conventional`.
- [ ] Add Husky `commit-msg` (commitlint) and `pre-commit` (`lint-staged`). `lint-staged` runs Prettier on markdown (`*.md`) only. Add `prettier.config.js`. Do not add a `pre-push` hook. Native builds stay on CI. Do not format `*.mdc` yet; **M7** teaches Prettier about those files when the rules exist.
- [ ] Append `node_modules/` to `.gitignore`. Commit `package-lock.json` and the hook scripts. Ignore any other output Husky generates that its own docs say not to commit. Do not add `.cursorignore` for these paths.
- [ ] In `README.md`, state that this repository is not a JavaScript app and that the root `package.json` exists for hooks and commitlint. Mention `npm install` so the hooks install.

**Non-goals:** no app changes, no GitHub Actions, no Cursor rules. Do not start **M6**.

**Close-out:** Prepend **M5** under **Shipped**. Move **M6** into **Now**. Delete this **M5** section.

### M6 — `ci: build both apps`

**Already exists:** both apps and commit hooks. README already lists the local format and build commands from **M3** and **M4**. No `.github/workflows/` yet.

**Acceptance:**

- [ ] Add a GitHub Actions workflow that runs on push to `main` and on pull requests. Use the same concurrency as better-saas: `group: ${{ github.workflow }}-${{ github.ref }}` and `cancel-in-progress: true`.
- [ ] On `macos-latest`, run the Swift format check and the `xcodebuild` build command already written in the README.
- [ ] On `ubuntu-latest`, run the `ktlint` and Gradle build tasks already written in the README.
- [ ] Keep the README command list equal to the commands the workflow runs.

**Non-goals:** no tests, no new product behavior, no `pre-push` hook, no vendor SDK, no extra jobs, no Cursor rules. Do not start **M7**.

**Close-out:** Prepend **M6** under **Shipped**. Move **M7** into **Now**. Delete this **M6** section.

### M7 — `chore: add cursor rules`

**Already exists:** both apps, commit hooks, and CI. README commands match `.github/workflows/ci.yml`. There is no `.cursor/rules/` yet.

Copy these files from `main` (do not type them from memory):

- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/conventions.mdc`
- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/changelog.mdc`
- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/review-staged.mdc`
- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/review-pr.mdc`

Keep the git, commit-message, secrets, and review procedure from those files. Do not invent a different policy. The five review criteria, the glance verdict, and “agents do not mutate git” stay. Remove Svelte and web-stack examples as specified below. Where those files name Bun, ESLint, Vitest, or `bun` CI steps, name the commands this repo already runs.

**Acceptance:**

- [ ] Add `.cursor/rules/conventions.mdc`. Keep **Secrets**, **Commit messages**, and **Git** as copied. In **Paths and file names**, keep lowercase kebab-case for repo paths, delete SvelteKit route names and `src/` TypeScript examples, and state that Swift and Kotlin files use each platform’s usual names. Replace the **Tooling** bullets that name Bun, ESLint, svelte-check, Vitest, or `bun run build` with the commands already in the README and in `.github/workflows/ci.yml`: the Swift format check, the `xcodebuild` build, `ktlint`, and the Gradle debug build. State that the root `package.json` is npm for hooks and commitlint, not the app. Do not add a test command. Keep the Markdown sentences that link `prettier.config.js` and `lint-staged.config.js`.
- [ ] Teach Prettier and lint-staged to format `*.mdc` with the Markdown parser, the way better-saas did when its rules landed. Markdown (`*.md`) stays as **M5** configured it.
- [ ] Add `.cursor/rules/changelog.mdc` as copied. It already matches this queue: when every **Now** acceptance box is `[x]`, ship in the same change.
- [ ] Add `.cursor/rules/review-staged.mdc`. Keep the staged-diff procedure, five criteria, fix-now versus leave-it, and glance shape. Delete Svelte, SvelteKit, Bun, Neon, Better Auth, Drizzle, and Vercel examples. Do not add keystores or provisioning profiles. Point **Design fit** at `docs/engineering.md`. When the staged diff touches `apps/`, the root hook package, the lockfile, or CI, run the README commands that apply to that diff. A docs-only or rules-only review says in one line that gates were skipped.
- [ ] Add `.cursor/rules/review-pr.mdc`. Keep the branch procedure and the same five criteria. Replace the `bun` CI command list with the steps `.github/workflows/ci.yml` runs. **🔴** if a required step fails. A docs-only or rules-only review notes that gates were skipped. Replace web route, auth, and schema examples with the contracts already in `docs/engineering.md`: bundle id and minimum OS.
- [ ] Add `.cursor/rules/parity.mdc` (`alwaysApply: true`). `docs/features/*.md` is the behavior contract. A change updates the spec and both apps in the same milestone, or **Now** names the platform that is behind. Do not implement behavior that is not in a feature spec.
- [ ] In `AGENTS.md`, add the review triggers: **review staged** → `review-staged.mdc`, **review branch** / PR → `review-pr.mdc`, **ship milestone** → `changelog.mdc`. Natural language is enough. Name the blocking gates that already exist: pre-commit (`lint-staged`), commitlint, and the CI commands. There is no `pre-push` hook.

**Non-goals:** no feature spec, no app behavior changes, no new CI jobs. Do not start **M8**.

**Close-out:** Prepend **M7** under **Shipped**. Move **M8** into **Now**. Delete this **M7** section.

### M8 — `docs: mark starter ready`

**Already exists:** both apps, hooks, CI, and Cursor rules. **Shipped** lists **M1–M7**.

**Acceptance:**

- [ ] Update `README.md` so a new clone is: clone the repo, `npm install`, then the same commands CI runs (Swift format check, `xcodebuild` build, `ktlint`, Gradle build).
- [ ] In `docs/engineering.md`, state that a product copies this repo, renames the apps, and keeps `docs/`, `AGENTS.md`, and `.cursor/rules/`. The template stops at two apps that build and ships no screen. Keep the local-records and preferences rows. Further product work is recorded in that repo’s `docs/engineering.md` and `docs/features/*.md` before code. The next milestone in the copied app is **M1**. Do not add the better-saas web stack (auth secret, Postgres, email auth, Vercel, Svelte skills, Svelte MCP).
- [ ] In `AGENTS.md`, remove the starter-only ban that blocks product work through **M8**. Point ongoing work at **Now**. This template does not grow product features in place; a product repo does.
- [ ] Clear `CHANGELOG.md` **Shipped** so it is empty (`_(none yet)_`). Remove every starter **M1–M8** entry.
- [ ] Replace this file with the empty queue below. Delete **How to run a milestone**, **Out of scope**, every milestone card, and **Contracts** if it is still here.

Empty queue to leave in this file:

```markdown
# Roadmap

> **M#** = engineering milestone. Shipped: [`CHANGELOG.md`](../CHANGELOG.md). Stack and layout: [`engineering.md`](engineering.md).

**Tracking:** Open work lives in **Now** / **Upcoming** / **Later** below; **Shipped** lives in [`CHANGELOG.md`](../CHANGELOG.md) only. Other docs must not name the active milestone — link here or to the changelog instead.

One milestone per commit; do not ship work past **Now** while that milestone is open.

## Now

No open milestone.

## Upcoming

_(none)_

## Later

_(none)_
```

**Non-goals:** no new app behavior. Do not add a product milestone. `plan.md` is already gone; do not recreate it.

**Close-out:** The empty **Shipped** section and the empty queue above are the close-out. There is no next id.

## Later

_(none)_
