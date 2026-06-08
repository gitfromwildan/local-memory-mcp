---
name: task-management-guidelines
description: Task tracking & progress management standards.
arguments: []
agent: Project Manager
category: workflows
version: "1.0.0"
tags: [workflow, tasks, status-management, mcp]
---

## Task Lifecycle

Entry=S0 → S1 → S2 → S3 → S4 → S5 Exit=done|archived
Guard: S(N) req S(N-1)✅; MUST transition backlog/pending → in_progress → completed

S0 | plan: task-create for full lifecycle (Research→Strategy→Execution→Validation) | — | tasks | —
S1 | claim: task-claim with task_code; inspect via claim-list | S0✅, not claimed by others | ownership | —
S2 | progress: task-update → in_progress | S1✅ | active work | —
S3 | validate: tests pass / explicit doc why verification skipped | S2✅ | evidence | —
S4 | complete: task-update → completed (auto-releases claims, expires handoffs, archives) | S3✅ | completion | —
S5 | verify: confirm completion evidence documented, auto-cleanup triggered | S4✅ | verified | —

## Navigation

Entry=S0 → S1 → S2 → S3 Exit=mutated
Guard: S(N) req S(N-1)✅

S0 | list: task-list (in_progress, pending) | — | pointer table | —
S1 | detail: task-detail after selecting (includes claims + handoffs) | S0✅ | full context | —
S2 | mutate: task-create | task-update | task-delete | S1✅ | changed | —
S3 | verify: confirm mutation succeeded, check task-list reflects change | S2✅ | verified | —

## Navigation (task-list)

- Sync: Call task-list at every session start (default: in_progress,pending).
- Format: Compact pointer table: id, task_code, title, status, priority, updated_at, comments_count. Use query for keyword search.
- Priority Scale: Interpret priority with MCP semantics: 1=Low, 2=Normal, 3=Medium, 4=High, 5=Critical.
- Retrieve: Fetch full context via task-detail AFTER selecting a task. Hydrated task includes current coordination state (active claims, pending handoffs).
- Coordination: Check active ownership with task-claim and claim-list. NEVER work on tasks claimed by others. Focus on ONE task at a time.

## Detail Tools

- Tasks: Call task-detail for history/comments (ID or task_code).
- Memory: Call memory-detail for full entry content.
- Standards: Call standard-search before any code edit, test edit, refactor, migration, or implementation decision. If no relevant standards returned, note that.
- Handoffs: Call handoff-list to discover pending context transfers before starting a task. Close stale handoffs with handoff-update.

## Workflow Rules

- Planning: Create tasks for full lifecycle (Research → Strategy → Execution → Validation).
- Transition Safety: MUST move from backlog/pending → in_progress → completed. Skipping in_progress is forbidden.
- Automatic Cleanup: task-update to completed or canceled automatically releases active claims and expires pending handoffs linked to that task.
- Claiming: Use task-claim when taking ownership, with task_code when working from human-visible queues.
- Claim Inspection: Use claim-list when ownership is unclear or when triaging stale work.
- Claim Release: Use claim-release to clear stale ownership when a task is being handed back or reassigned.
- Handoff: Use handoff-create only when pausing or transferring unfinished work. Do not use pending handoffs for completion summaries.
- Validation: Only mark completed after passing tests or explicitly documenting why verification could not run.
- Archiving: Completion triggers auto-archive to task_archive memory with token reporting.
