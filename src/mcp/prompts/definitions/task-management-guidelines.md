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

Entry=S0 → S1 → S2 → S3 → S4 → S5   Exit=done|archived
Guard: S(N) req S(N-1)✅; MUST transition backlog/pending → in_progress → completed

S0 | plan: task-create for full lifecycle (Research→Strategy→Execution→Validation) | — | tasks | —
S1 | claim: task-claim with task_code; inspect via claim-list | S0✅, not claimed by others | ownership | —
S2 | progress: task-update → in_progress | S1✅ | active work | —
S3 | validate: tests pass / explicit doc why verification skipped | S2✅ | evidence | —
S4 | complete: task-update → completed (auto-releases claims, expires handoffs, archives) | S3✅ | completion | —
S5 | verify: confirm completion evidence documented, auto-cleanup triggered | S4✅ | verified | —

## Navigation

Entry=S0 → S1 → S2 → S3   Exit=mutated
Guard: S(N) req S(N-1)✅

S0 | list: task-list (in_progress, pending) | — | pointer table | —
S1 | detail: task-detail after selecting (includes claims + handoffs) | S0✅ | full context | —
S2 | mutate: task-create | task-update | task-delete | S1✅ | changed | —
S3 | verify: confirm mutation succeeded, check task-list reflects change | S2✅ | verified | —
