<!-- ai-rules:start | managed by jazkng/ai-rules, edit there, not here -->
# Shared AI rules (jazkng)

Applies to every AI coding agent (Claude Code, Codex, Gemini, Antigravity, others) in every project.
Project-specific rules live in the "Project rules" section of each repo's AGENTS.md and override these when they conflict.

## Communication
- Reply to Jake in Simplified Chinese. Keep code identifiers, file names and commands in English.
- Be concise: lead with the result, no step-by-step recap.
- If the request is unclear and costly to redo, ask first. Otherwise proceed and state the assumption you made.

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
- If code structure changed and graphify is set up, run `graphify update .` before the final commit.

### Merging and releasing
- When all checks pass, merge your own PR into the base branch yourself. No command from Jake is needed.
  - One-branch project (only `main`): merging is the release.
  - Two-branch project (a preview branch plus `main`, named in its project rules): merging updates the preview / test site only.
- 「发布」 is the only command: in a two-branch project, release the preview branch to production (merge it into `main`, or run the project's release workflow) only when Jake says 「发布」 in the conversation.
- Never merge a PR whose checks fail. Report the failure instead, even if it looks unrelated to your change.
- On 「发布」 in a two-branch project, also create a GitHub Release on the released commit: tag `vYYYY.MM.DD` (add `.2`, `.3` for later releases the same day), title the same, notes in Chinese with one line per PR included since the previous release. One-branch projects do not create Releases.

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
