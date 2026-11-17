# Project memory

This file is shared by Codex, Claude Code and Antigravity through Git. Read it before continuing work; update important verified results before handing off. Keep entries concise and project-specific. Central rule synchronization creates this file only when absent and never replaces existing content.

## Entry format

Use stable project-scoped IDs. Date format: YYYY-MM-DD; include timezone for precise times. Source should identify a user decision, repository file, PR, commit, build or other inspectable evidence. No secrets or unnecessary personal/customer details.

Statuses: proposed, user-confirmed, verified, pending, completed, superseded. A user-confirmed intention is not proof of installation, a signed agreement, deployment or acceptance.

| ID | Date | Category | Status | Fact / decision | Source | Next action |
|---|---|---|---|---|---|---|
| MAINT-20261118-001 | 2026-11-18 | Repository hygiene | pending | Add missing .gitignore for local secrets, generated tooling output and operating-system files; retain application and policy content. | GitHub maintenance request; .gitignore. | Verify PR checks and merge; this change does not verify deployment or change runtime data. |

## Current work

Record the active goal, verified progress, blockers and next step when known. No project facts have been seeded by the central template.

## Superseded decisions

Retain the old ID, the replacement ID and the reason/date when a material decision changes. Reconcile conflicts explicitly; preserve unrelated entries when merging concurrent updates.
