# <project-name> Agent Guide

## Project Positioning

- <One-sentence project purpose.>
- Current stack: <frameworks, languages, tests, database, deployment>.
- Core capabilities: <main features>.
- Test principle: <mock external services, avoid production calls, etc.>.

## First-Read Entrypoints

- Human project overview and setup: `README.md`
- Documentation index: `docs/README.md`
- Stable references: `docs/reference/`

## Directory Map

- `<path>`: <responsibility>
- `<path>`: <responsibility>

## Architecture Boundaries

- <Client/server boundary.>
- <Data access boundary.>
- <External service/provider boundary.>
- <State, cache, or persistence boundary.>

## Safety and Configuration

- Do not commit real `.env`, API keys, databases, generated media, runtime data, or user-private content.
- Environment variables are defined by `.env.example` and config parsing code.
- <Project-specific safety rules.>

## Common Verification

- Install dependencies: `<command>`
- Local development: `<command>`
- Lint: `<command>`
- Typecheck: `<command>`
- Test: `<command>`
- Build: `<command>`
- Whitespace check: `git diff --check`

## Verification Tradeoffs

- <Small UI/content changes: relevant minimal checks.>
- <API/data/auth/config changes: targeted tests and broader checks.>
- <Deployment/config/build changes: build or smoke checks.>

## Documentation Update Triggers

Before finishing a change, check whether documentation needs updates if this change:

- Changes module responsibilities, directory structure, architecture boundaries, or data flow.
- Changes auth, user isolation, secrets, external service configuration, or data retention.
- Adds, removes, or renames environment variables, deployment commands, verification commands, or production operations.
- Adds stable capabilities, public APIs, data tables, provider types, or durable business rules.
- Reveals that `AGENTS.md`, `README.md`, `docs/README.md`, or `docs/reference/` is stale.

Update priority:

- Agent workflow, directory map, or architecture boundaries: update `AGENTS.md`.
- Documentation entrypoints, directory status, or historical status: update `docs/README.md`.
- Long-lived system facts: update `docs/reference/`.
- Setup, run, deployment, or environment variables: update `README.md` and necessary `.env.example` files.
- Phase-specific design, planning, review, or release records: add `docs/specs/`, `docs/plans/`, or `docs/reports/`.

For local-only bugfixes, small text changes, style tweaks, or test-only refactors, usually do not update docs; mention that no long-lived documentation changed.
