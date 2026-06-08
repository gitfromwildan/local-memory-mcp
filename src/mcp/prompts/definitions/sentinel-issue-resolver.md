---
name: sentinel-issue-resolver
description: Resolve GitHub issues autonomously with deep context analysis and structured commits.
arguments:
  - name: issue_url
    description: The full URL of the GitHub issue to resolve.
    required: true
agent: SENTINEL Issue Resolver
category: workflows
version: "1.0.0"
tags: [workflow, github, issue-resolution, sentinel]
---

## Sentinel Issue Resolver

Entry=S0 → S1 → S2 → S3 → S4 → S5 → S6 → S7 → S8 → S9 Exit=resolved
Guard: S(N) req S(N-1)✅; autonomous — no permission per step
Hint: If repo not auto-detected from issue_url, run `git remote -v` to get owner/repo from origin URL.

S0 | fetch: issue_read body + ALL comments (get_comments) | issue_url provided? | raw issue + all comments | —
S1 | analyze comments: extract requirements, hints, root cause clues, reproduction steps, error details | S0✅ | comment analysis | —
S2 | detect attachments: parse all comments for image/video markdown URLs, linked assets | S1✅ | attachment URL list | —
S3 | download: gh CLI (gh issue view, gh api) to fetch each attachment — private repo, NO curl | S2✅ & attachments exist? | local files | —
S4 | analyze attachments: inspect screenshots/videos for UI bugs, error states, configs, visual hints | S3✅ | attachment analysis | —
S5 | research: memory-search + standard-search + codebase exploration (trace call sites, read docs) | S0-4✅ | full context | —
S6 | register: task-create (link issue URL) + task-claim + task-update→in_progress | S5✅ | MCP task | —
S7 | implement fix + validate: tests, linters, e2e | S6✅ | verified changes | —
S8 | finalize: commit (type(scope): msg — fix #N) + task-update→completed + issue comment summary | S7✅ | resolution | —
S9 | verify: confirm commit pushed, issue comment posted, task marked completed | S8✅ | verified | —

Target: {{issue_url}}
