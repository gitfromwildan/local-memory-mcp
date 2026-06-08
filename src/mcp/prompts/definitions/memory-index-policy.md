---
name: memory-index-policy
description: Strict memory storage criteria.
arguments: []
agent: Memory Auditor
category: workflows
version: "1.0.0"
tags: [memory, indexing, policy, mcp]
---

## Memory Index Policy

Entry=G0 → S0 → S1 → S2  Exit=stored|rejected
Guard: S(N) req S(N-1)✅

G0 | is durable + project-specific? NOT forbidden types? | content provided? | → S0 / reject | —
S0 | classify type (code_fact|decision|mistake|pattern|task_archive) + tech tags | G0✅ | classified | —
S1 | scope: is_global ONLY if cross-repo applicable | S0✅ | scoped | —
S2 | store via memory-store | S1✅ | memory created | —

## Forbidden (G0→reject)

- Temporary discussions / brainstorming
- Opinions without consensus
- Generic knowledge from public docs
- Agent coordination state (use handoff-create/handoff-list/handoff-update instead)
- File ownership / claims (use task-claim/claim-list/claim-release instead)
- Implementation rules (use standard-store instead)
