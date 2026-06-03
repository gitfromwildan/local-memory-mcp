---
name: documentation-sync
description: Sync memory decisions with repository markdown files
arguments: []
agent: Documentation Specialist
category: workflows
version: "1.0.0"
tags: [workflow, documentation, memory, sync]
---

## FSM

Entry=S0 → S1 → S2 → S3 Exit=aligned
Guard: S(N) req S(N-1)✅

S0 | search decision memories via memory-search | — | memory entries | —
S1 | read_file(README.md) + glob & read_file(docs/**/\*.md, .agents/documents/**/_, .kiro/\*\*/_) | S0✅ | doc content | —
S2 | compare: identify missing/outdated knowledge | S1✅ | gap list | —
S3 | propose specific changes to align docs | S2✅ | update proposals | —
