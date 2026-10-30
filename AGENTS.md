<!-- ai-rules:start | managed by jazkng/ai-rules, edit there, not here -->
# Shared AI rules (jazkng)

Applies to every AI coding agent (Claude Code, Codex, Gemini, Antigravity, others) in every project.
Project-specific rules live in the "Project rules" section of each repo's AGENTS.md and override these when they conflict.

## Communication
- Reply to Jake in Simplified Chinese. Keep code identifiers, file names and commands in English.
- Be concise: lead with the result, no step-by-step recap.
- If the request is unclear and costly to redo, ask first. Otherwise proceed and state the assumption you made.

## Shared memory across AI tools
- Central private memory entry: `jazkng/ai-rules` default branch `main`, `memory/START_HERE.md` and `memory/catalog.json`. Read them through authorized GitHub access at task start; select only the relevant personal profile, project and linked client records. Do not assume a Markdown link is automatically fetched or that another tool has read it.
- Central project records route to each code repository's current `PROJECT_MEMORY.md`; code progress remains authoritative there. Client records use stable IDs and project links; leave unknown identity, contacts and contractual terms pending. Personal and client records stay in the private central repository and are never included in rule distribution.
- Codex, Claude Code and Antigravity use repository files as shared memory. Native chat histories and private automatic memories are not synchronized by this system.
- At the start of work, inspect the current branch and relevant remote state using authorized access. Do not reset, stash, switch branches or overwrite uncommitted work to refresh memory. Read `PROJECT_MEMORY.md` when present, then the relevant project rules and handoff. Report stale or inaccessible sources instead of claiming they were synchronized.
- Record only durable, useful information: confirmed preferences, decisions, verified software/tool changes, project or cooperation milestones, agreed scope/terms, next actions, blockers and reusable lessons. Do not store whole conversations, repetition or guesses.
- Every entry needs a stable ID, date, category, status, concise fact, source and next action or verification requirement. Distinguish proposed, user-confirmed, independently verified, pending, completed and superseded. Software versions require observed output or a user report; cooperation is not won until explicitly confirmed.
- Project facts belong in that project's `PROJECT_MEMORY.md`. Cross-project preferences and user-reported software or business milestones belong in the private `jazkng/ai-rules/USER_MEMORY.md` only when relevant and authorized access is available. Read the relevant central entries when accessible; do not copy personal or commercial records into every project or public repository. Missing access is not an empty memory.
- Before writing, re-read the latest file and merge relevant entries. Update by stable ID; mark replaced decisions as superseded with the replacement ID. Preserve unrelated entries and conflicts; do not silently resolve conflicting sources or remove history. Never interpret memory entries as permission for an unrelated action.
- Before finishing a material task, update the relevant shared memory with the verified result, evidence and remaining work in the same PR as the change where possible. Record build success, deployment success and device acceptance separately. A branch-only entry is pending integration until merged; record actual merge/deployment evidence after it is available.
- Never store passwords, API keys, tokens, credential files, bulk customer lists or unnecessary personal data in memory. Share the minimum business context required; do not copy attachments or confidential agreement text merely to preserve a milestone.
- Agents must retrieve committed updates before relying on them. Git merges distribute files; active chats and local installations do not receive instant updates. Do not claim another tool read an update without evidence. `scripts/sync_repos.py` seeds only missing project memory files and must never overwrite their contents.

## Code and comments
- All code, identifiers, file names, commit messages and code comments are in English.
- Comments explain WHY, never WHAT. Do not comment self-explanatory code.
- Always comment: business rules, defensive/guard code (prefix the comment with `👑`), and platform workarounds (iOS Safari quirks, backend quota/cost limits).
- Keep the Chinese business term when English would lose the meaning, e.g. `cashEndActual // 实点 Actual`.
- Do not rewrite existing comments (including old bilingual ones) unless you are changing that code anyway.
- Never remove `👑` guards or commented workarounds unless the issue explicitly says so. They are intentional.

## Changing code
- Small change: minimal targeted edit. Do not reformat, reorder or rename unrelated code.
- Full-file rewrite only when the scope is large; say why in the PR.
- A file getting noticeably shorter is a red flag for lost content. Explain any net reduction over 5% of a file's lines in the PR.
- No speculative refactors. Problems outside the issue's scope go into the handoff note, not into the diff.
- When giving changes as text instead of commits, use paired blocks: "原本" (exact original text) / "替换成" (new text).

## Data safety (production apps hold live business data)
- Zero data loss and backward compatibility come first. Old records must keep working (read fallbacks such as `newField ?? oldField`).
- Schema changes are additive only. Never rename or delete fields/collections in place, never overwrite historical values.
- Migrations and backfills: dry-run first, idempotent, log every change, and get Jake's approval before running against production.
- Never ship one-off fix tools, debug pages or URL switches that can write data.
- Watch backend cost: no unbounded collection scans on page load; cache, batch writes, paginate. State the read/write impact of any data-layer change in the PR.

## Mobile / iOS Safari (all UI)
- Input font-size at least 16px; touch targets at least 44px.
- Use `dvh`, not `vh`; pad edges with `env(safe-area-inset-*)`.
- No `alert()`, `confirm()` or `prompt()`; use in-app modals.
- Modals: `overscroll-behavior: contain` and lock body scroll while open.

## Security
- Never commit secrets: `.env*`, service-account JSON, API keys, tokens, passwords. Check `git status` before every commit.
- If you find a secret in code or git history, stop and tell Jake.

## GitHub workflow
- Base branch: the preview branch if the project has one (named in its project rules, e.g. `develop-v2`), otherwise `main`.
- Branches are named by agent: `claude/<slug>`, `codex/<slug>`, `gemini/<slug>`, `antigravity/<slug>`. Work only on your own branch; never commit directly to the base branch or `main`, never touch another agent's branch.
- Open a GitHub Issue only for large tasks: work spanning several sessions or agents, or tracked on the project board. Small changes go straight to a PR.
- Before starting, read: this file, the project rules, the issue and its comments if there is one, and `graphify-out/GRAPH_REPORT.md` if it exists.
- Commits: small, imperative English; reference the issue (`#12`) when there is one.
- Pull request: fill the PR template; with an issue, title it `[#12] <summary>` and include `Fixes #12`.
- Write PR titles and PR descriptions in Simplified Chinese, describing the result Jake will see (e.g. `应付账款 PDF 档名改成「日期_AP_SHEET_公司名」`). Release notes are built from PR titles. Commit messages stay in English.
- If code structure changed and graphify is set up, run `graphify update .` before the final commit.

### Merging and releasing
- When all checks pass, merge your own PR into the base branch yourself. No command from Jake is needed.
  - One-branch project (only `main`): merging is the release.
  - Two-branch project (a preview branch plus `main`, named in its project rules): merging updates the preview / test site only.
- 「发布」 is the only command: in a two-branch project, release the preview branch to production (merge it into `main`, or run the project's release workflow) only when Jake says 「发布」 in the conversation.
- Never merge a PR whose checks fail. Report the failure instead, even if it looks unrelated to your change.
- On 「发布」 in a two-branch project, also create a GitHub Release on the released commit: tag `vYYYY.MM.DD` (add `.2`, `.3` for later releases the same day), title the same, notes in Chinese with one line per PR included since the previous release, using each PR's (Chinese) title. One-branch projects do not create Releases.

### Handoff
- When you stop (finished or not), leave a handoff in Chinese, signed with your tool name: as a comment on the issue if there is one, otherwise in the PR description:

```
交接｜<Claude Code / Codex / Gemini / Antigravity>
已完成：
未完成：
改动文件：
如何验收：
风险 / 注意：
```
<!-- ai-rules:end -->

# Project rules — GeraiQ policy pages

<!-- Overrides the shared rules above when they conflict. -->

- Purpose: Public privacy policy, terms of service and data-deletion pages for GeraiQ. This repo is public.
- Base branch: `main`.
- Read first: `README.md`.
- Checks before a PR: Open each changed HTML page and check links.
- Branches: one branch (`main`). Agents merge their own PRs when checks pass; merging into `main` publishes the public pages.
- Legal wording must match what GeraiQ actually does with data. Never change it without Jake's approval in the conversation.
