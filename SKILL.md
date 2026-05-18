---
name: project-agent-docs
description: Create or improve an agent-friendly project documentation system for new or existing codebases. Use when initializing a repository for Codex/agent work, adding or updating AGENTS.md, creating docs/README.md, organizing docs/reference/*, marking historical docs, defining architecture boundaries, verification commands, and documentation update triggers.
---

# Project Agent Docs

## Purpose

Use this skill to bootstrap or repair the small set of project documents that help Codex work reliably in a repository:

- `AGENTS.md`: the agent-facing project map, constraints, validation rules, and documentation update triggers.
- `docs/README.md`: the documentation index and "current truth" entrypoint for the docs tree.
- `docs/reference/*`: stable, currently valid system facts that future agents can reuse.

Keep the system lightweight. Do not create documents just to satisfy a template.

## Core Rules

- Inspect the repository before writing. Read existing README files, package/build config, source tree, tests, and existing docs.
- Do not invent project facts. If a boundary, command, or feature cannot be verified from the repo, omit it or mark it as a recommendation.
- Use the repository's primary language for generated project-facing documents. If the user communicates in Chinese or the repository has Chinese AGENTS/README/docs, generate Chinese documentation.
- Preserve existing useful documentation. Mark historical or obsolete docs clearly instead of deleting or rewriting them unless the user asks.
- Prefer updating existing files over adding parallel duplicates.
- Keep generated docs concise and navigational. Detailed product plans belong in specs/plans, not in `AGENTS.md`.
- Do not include real secrets, API keys, database dumps, generated media, runtime data, or user-private content.

## Workflow

1. **Inventory the project**
   - Check for existing `AGENTS.md`, `README*`, `docs/`, source directories, tests, dependency manifests, environment examples, CI/build config, and deployment files.
   - Identify the primary language, tech stack, module boundaries, validation commands, security-sensitive areas, and external services.

2. **Classify the repository state**
   - New or small project: create the smallest useful set, usually `AGENTS.md` and optionally `docs/README.md`.
   - Existing project with docs: add entrypoints, classify docs, and mark historical material.
   - Mature project: consolidate stable facts into `docs/reference/` and keep historical specs/plans as traceable records.

3. **Create or update `AGENTS.md`**
   - Include project positioning, first-read entrypoints, directory map, architecture boundaries, safety/config rules, validation commands, validation tradeoffs, and documentation update triggers.
   - Do not copy long README content into `AGENTS.md`; link to it.
   - Use `assets/AGENTS.template.md` as a structure reference when useful.

4. **Create or update `docs/README.md`**
   - Explain which docs are current entrypoints and which are historical records.
   - Describe the docs directory topology.
   - Use `assets/docs-README.template.md` as a structure reference when useful.

5. **Create `docs/reference/*` only when useful**
   - Add reference files only when there is verified, stable content worth preserving.
   - Use `assets/reference-architecture.template.md` and `assets/reference-data-and-storage.template.md` as optional starting points.
   - Prefer "recommended future additions" in `docs/README.md` over empty reference files.

6. **Mark historical docs**
   - For old controller prompts, obsolete plans, stale specs, or legacy handoff docs, add a short top note such as:
     `Historical record only. Current project entrypoints are AGENTS.md, README.md, and docs/README.md.`
   - Move to `docs/archive/` only when the user wants file reorganization or references are easy to update.

7. **Verify and report**
   - Run a lightweight text check such as `git diff --check`.
   - Report what was created/updated, which files are current entrypoints, and whether any docs remain historical or uncertain.

## Recommended Docs Topology

Use this topology as a recommendation, not a rigid requirement:

```text
docs/
  README.md                 # Documentation index and current docs entrypoint
  reference/                # Stable, currently valid system facts
    architecture.md         # Module responsibilities, boundaries, data flow
    data-and-storage.md     # Persistence, privacy, retention, backups
    auth-and-security.md    # Auth, permissions, secrets, user isolation
    external-services.md    # Third-party APIs, providers, webhooks, integrations
    verification.md         # Test/build/smoke/release verification strategy
  specs/                    # Product/design specs, usually date-prefixed
  plans/                    # Implementation plans and task breakdowns
  reports/                  # Reviews, validation reports, release checks, incidents
  archive/                  # Historical or obsolete material kept for traceability
```

Create only directories and files that have real value now. Do not create empty reference files to match the topology.

## What Goes Where

- `AGENTS.md`: how an agent should work in this repo; directory map; boundaries; validation; doc update triggers.
- `README.md`: human-facing project overview, setup, run, deployment, and user-relevant operations.
- `docs/README.md`: documentation index and status map.
- `docs/reference/`: durable system truths that should stay current.
- `docs/specs/`: product/design decisions for a phase, often date-prefixed.
- `docs/plans/`: execution plans and task breakdowns, usually historical after completion.
- `docs/reports/`: reviews, verification results, release checks, incident reviews.
- `docs/archive/`: old material retained for traceability.

## Documentation Update Triggers

Include this logic in generated `AGENTS.md`, adapted to the project:

- Before finishing a change, check whether docs need updates if the change modifies module responsibilities, directory structure, architecture boundaries, data flow, auth, user isolation, secrets, external service config, data retention, environment variables, deployment commands, validation commands, public APIs, data tables, provider types, or stable business rules.
- Update `AGENTS.md` for agent workflow, directory map, or architecture boundary changes.
- Update `docs/README.md` for documentation entrypoint, directory status, or historical status changes.
- Update `docs/reference/` for long-lived system facts.
- Update `README.md` and `.env.example` for setup, run, deployment, or environment variable changes.
- Add `docs/specs/`, `docs/plans/`, or `docs/reports/` entries for phase-specific design, planning, review, or release records.
- Do not update docs for local-only bugfixes, small text changes, style tweaks, or test-only refactors unless they reveal stale documentation.

## Output Expectations

When finished, summarize:

- Files created or changed.
- Current project entrypoints.
- Any historical docs that were marked or left untouched.
- Verification performed.
- Any stable facts that could not be confidently documented.
