# Agent instructions

Humans: [`README.md`](README.md). This file is for Cursor and coding agents. Work stays on [**Now**](docs/roadmap.md#now) unless the user asks for more.

## Working context

- **Now:** [`docs/roadmap.md#now`](docs/roadmap.md#now)
- **Upcoming / Later:** [`docs/roadmap.md`](docs/roadmap.md)
- **Shipped milestones:** [`CHANGELOG.md`](CHANGELOG.md)
- **Contracts, layout, and OS pins:** [`docs/engineering.md`](docs/engineering.md)

## Git

Read-only unless the user’s current message explicitly requests that command.

Allowed inspection: `git status`, `git diff`, `git diff --cached`, `git log`, `git show`, and listing branches.

Mutating commands (`git add`, `git commit`, `git push`, and the rest) wait for an explicit request. Staging is the user’s job. When asked for a commit message, output text only unless they also asked to commit.

## Commit messages

Conventional Commits. Imperative lowercase summary. No trailing period.

One change is the subject only. More than one change is a blank line and `- ` bullets. Do not mention changelog entries or advancing **Now** in the body.

## Scope

While [`docs/roadmap.md`](docs/roadmap.md) still lists starter milestones, do not add product features, vendor SDKs, or an asset pipeline.
