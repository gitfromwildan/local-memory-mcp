---
name: server-instructions
description: Main instructions for the MCP server
---

Local Memory MCP — persistent memory, task coordination, and coding standards for AI agents.

## Session Start FSM

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

- `session-planner` — orient and plan at session start
- `task-memory-executor` — execute tasks with memory and standard enforcement
- `senior-code-review` — full code review against stored standards
- `memory-guided-review` — review using project memory as context
- `architecture-design` — architectural planning and ADR generation
- `technical-planning` — feature planning with task decomposition
- `root-cause-analysis` — structured bug / incident investigation
- `fix-suggestion` — propose and validate fixes
- `security-triage` — security risk assessment
- `sentinel-issue-resolver` — autonomous GitHub issue resolution (SENTINEL identity)
- `learning-retrospective` — capture lessons and update memory
- `documentation-sync` — sync docs with current codebase state
- `project-briefing` — generate repository briefing from memory
