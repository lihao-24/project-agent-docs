# <project-name> Documentation Index

This directory stores project knowledge and historical records. Current development entrypoints are the root `AGENTS.md`, `README.md`, and this index.

## Read First

- Project overview, setup, and operations: `../README.md`
- Agent workflow, directory map, and boundaries: `../AGENTS.md`
- Stable architecture reference: `reference/architecture.md`
- Data and storage reference: `reference/data-and-storage.md`

## Directory Guide

- `reference/`: stable, currently valid system facts.
- `specs/`: product and design specs, usually date-prefixed.
- `plans/`: implementation plans and task breakdowns; these may be historical after completion.
- `reports/`: reviews, validation reports, release checks, and incident reviews.
- `archive/`: historical or obsolete material kept for traceability.

## Maintenance Rules

- Put durable rules in `reference/`.
- Date-prefix temporary plans and design drafts.
- Mark obsolete material as historical before deleting it.
- Do not document real secrets, database dumps, runtime data, generated media, or private user content.
