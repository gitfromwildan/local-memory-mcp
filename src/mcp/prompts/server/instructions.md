---
name: server-instructions
description: Main instructions for the MCP server
---

Local Memory MCP — persistent memory, task coordination, and coding standards for AI agents.

## Session Start Mode

Entry=orient → hydrate → ready Guard: S(N) req S(N-1)✅

S0 | task-list (active/pending) + handoff-list(pending; close stale via handoff-update) | session start? | active tasks + transfers | —
S1 | memory-search + memory-synthesize (architectural context) + standard-search(MANDATORY before code/test/refactor/migrate — task intent, lang, stack, repo filters) | S0✅ | hydrated context | —
S2 | continue to task or respond | S1✅ | ready | —

## Core Workflows

**Memory**: memory-search → memory-detail → memory-store | memory-update

- Durable only (arch, patterns, decisions, fixes)
- memory-acknowledge after code gen from memory
- Global scope = cross-repo only; prefer repo-specific

**Tasks**: task-list → task-claim → task-update(in_progress) → task-update(completed)

- Register via task-create before execution
- NEVER skip in_progress
- Commit: `type(scope): [task-code] message` + `- [Title]` + `  [Summary]`
- Complete auto-releases claims + expires linked handoffs

**Standards**: standard-search → standard-store

- MANDATORY pre-implementation gate
- 1 rule/entry, normative contract

**Handoffs/Claims**: handoff-list → handoff-create | handoff-update | task-claim | claim-release

- Create ONLY for unfinished work (concrete next owner/steps)
- NO handoff for completion summaries → use task-update comments

## Available Prompts (slash commands)

- `architecture-design` — architectural planning and ADR generation
- `create-task` — create structured, atomic tasks in Local Memory MCP
- `csl-from-docs` — create atomic CSL coding standards entries from a local file or directory path
- `csl-scrapper` — scrape trusted documentation from a URL into atomic CSL coding standards entries
- `documentation-sync` — sync docs with current codebase state
- `export-task-to-github` — export local tasks to GitHub Issues
- `fix-suggestion` — propose and validate fixes
- `import-github-issues` — import GitHub Issues as local tasks
- `learning-retrospective` — capture lessons and update memory
- `memory-agent-core` — behavioral contract for memory-aware agents
- `memory-guided-review` — review using project memory as context
- `memory-index-policy` — strict memory storage criteria
- `project-briefing` — generate repository briefing from memory
- `review-and-audit` — audit documentation against implementation; generate local tasks for gaps
- `review-and-post-issue` — audit documentation against implementation; generate GitHub issues for gaps
- `root-cause-analysis` — structured bug / incident investigation
- `security-triage` — security risk assessment
- `senior-code-review` — full code review against stored standards
- `sentinel-issue-resolver` — autonomous GitHub issue resolution (SENTINEL identity)
- `session-planner` — orient and plan at session start
- `task-management-guidelines` — task tracking and progress management standards
- `task-memory-executor` — execute tasks with memory and standard enforcement
- `tech-affinity-scout` — scout best practices from similar tech projects
- `technical-planning` — feature planning with task decomposition
- `tool-usage-guidelines` — tool usage standards and data integrity
