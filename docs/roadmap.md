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

| Add in the product repo                            | Where it is recorded                                                                                                   |
| -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Product screens and behavior                       | `docs/features/<name>.md`, then iOS and Android                                                                        |
| On-device records and preferences                  | The SwiftData, Room, `AppStorage`, and DataStore choices in `docs/engineering.md`, then a feature spec, then both apps |
| A native library (SPM, Gradle, or a copied binary) | One pin (version or commit) in `docs/engineering.md`; both apps if both need it                                        |
| Build scripts that fetch or package assets         | `tools/`, invoked from the app build, not at runtime on the device                                                     |
| Large or generated assets                          | Gitignored; how to produce them is in `tools/` or engineering when the product adds them                               |
| Accounts, backend, sync, push, purchases           | Their own feature docs                                                                                                 |

If only one platform ships in a milestone, **Now** says so.

These better-saas pieces do not get a milestone here: auth secret, Postgres, email auth, Vercel, Svelte skills, and Svelte MCP. That is the web stack. Do not add them.

**M8** folds this boundary into `docs/engineering.md` and deletes this section.

## Now

### M6 — `ci: build both apps`

**Already exists:** both apps and commit hooks. README already lists the local format and build commands from **M3** and **M4**. No `.github/workflows/` yet.

**Acceptance:**

- [ ] Add a GitHub Actions workflow that runs on push to `main` and on pull requests. Use the same concurrency as better-saas: `group: ${{ github.workflow }}-${{ github.ref }}` and `cancel-in-progress: true`.
- [ ] On `macos-latest`, run the Swift format check and the `xcodebuild` build command already written in the README.
- [ ] On `ubuntu-latest`, run the `ktlint` and Gradle build tasks already written in the README.
- [ ] Keep the README command list equal to the commands the workflow runs.

**Non-goals:** no tests, no new product behavior, no `pre-push` hook, no vendor SDK, no extra jobs, no Cursor rules. Do not start **M7**.

**Close-out:** Prepend **M6** under **Shipped**. Move **M7** into **Now**. Delete this **M6** section.

## Upcoming

### M7 — `chore: add cursor rules`

**Already exists:** both apps, commit hooks, and CI. README commands match `.github/workflows/ci.yml`. There is no `.cursor/rules/` yet.

Copy these files from `main` (do not type them from memory):

- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/conventions.mdc`
- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/changelog.mdc`
- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/review-staged.mdc`
- `https://raw.githubusercontent.com/mislam/better-saas/main/.cursor/rules/review-pr.mdc`

Keep the git, commit-message, secrets, and review procedure from those files. Do not invent a different policy. The five review criteria, the glance verdict, and “agents do not mutate git” stay. Remove Svelte and web-stack examples as specified below. Keep Bun as the package manager (`packageManager` in `package.json`, `bun install`, `bunx` in hooks). Where those files name ESLint, Vitest, svelte-check, or app commands (`bun lint`, `bun check`, `bun run build`, `bun run test`), name the commands this repo already runs.

**Acceptance:**

- [ ] Add `.cursor/rules/conventions.mdc`. Keep **Secrets**, **Commit messages**, and **Git** as copied. In **Paths and file names**, keep lowercase kebab-case for repo paths, delete SvelteKit route names and `src/` TypeScript examples, and state that Swift and Kotlin files use each platform’s usual names. Keep the **Tooling** line that names Bun as the package manager. Replace the bullets that name ESLint, svelte-check, Vitest, `bun lint`, `bun check`, `bun run build`, or `bun run test` with the commands already in the README and in `.github/workflows/ci.yml`: the Swift format check, the `xcodebuild` build, `ktlint`, and the Gradle debug build. State that the root `package.json` is Bun for hooks and commitlint, not the app. Do not add a test command. Keep the Markdown sentences that link `prettier.config.js` and `lint-staged.config.js`.
- [ ] Teach Prettier and lint-staged to format `*.mdc` with the Markdown parser, the way better-saas did when its rules landed. Markdown (`*.md`) stays as **M5** configured it.
- [ ] Add `.cursor/rules/changelog.mdc` as copied. It already matches this queue: when every **Now** acceptance box is `[x]`, ship in the same change.
- [ ] Add `.cursor/rules/review-staged.mdc`. Keep the staged-diff procedure, five criteria, fix-now versus leave-it, and glance shape. Delete Svelte, SvelteKit, Neon, Better Auth, Drizzle, and Vercel examples. Keep Bun where it installs hooks (`bun install`, `bunx`). Do not add keystores or provisioning profiles. Point **Design fit** at `docs/engineering.md`. When the staged diff touches `apps/`, the root hook package, the lockfile, or CI, run the README commands that apply to that diff. A docs-only or rules-only review says in one line that gates were skipped.
- [ ] Add `.cursor/rules/review-pr.mdc`. Keep the branch procedure and the same five criteria. Replace the `bun` CI command list with the steps `.github/workflows/ci.yml` runs. **🔴** if a required step fails. A docs-only or rules-only review notes that gates were skipped. Replace web route, auth, and schema examples with the contracts already in `docs/engineering.md`: bundle id and minimum OS.
- [ ] Add `.cursor/rules/parity.mdc` (`alwaysApply: true`). `docs/features/*.md` is the behavior contract. A change updates the spec and both apps in the same milestone, or **Now** names the platform that is behind. Do not implement behavior that is not in a feature spec.
- [ ] In `AGENTS.md`, add the review triggers: **review staged** → `review-staged.mdc`, **review branch** / PR → `review-pr.mdc`, **ship milestone** → `changelog.mdc`. Natural language is enough. Name the blocking gates that already exist: pre-commit (`lint-staged`), commitlint, and the CI commands. There is no `pre-push` hook.

**Non-goals:** no feature spec, no app behavior changes, no new CI jobs. Do not start **M8**.

**Close-out:** Prepend **M7** under **Shipped**. Move **M8** into **Now**. Delete this **M7** section.

### M8 — `docs: mark starter ready`

**Already exists:** both apps, hooks, CI, and Cursor rules. **Shipped** lists **M1–M7**.

**Acceptance:**

- [ ] Update `README.md` so a new clone is: clone the repo, `bun install`, then the same commands CI runs (Swift format check, `xcodebuild` build, `ktlint`, Gradle build).
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
