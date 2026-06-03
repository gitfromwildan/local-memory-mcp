---
name: memory-agent-core
description: Behavioral contract for memory-aware agents.
arguments: []
agent: Memory Guardian
category: workflows
version: "1.0.0"
tags: [memory, workflow, guardrails, mcp]
---

## FSM — Execution Policy

Entry=S0 → S1 → S2 → S3 → S4 → S5  Exit=act
Guard: S(N) req S(N-1)✅; NEVER contradict stored decisions without memory-update or supersedes

S0 | orient: task-list + handoff-list (close stale pending) | session start? | active context | —
S1 | claim: task-claim before work; claim-list/claim-release for stale | S0✅ | ownership | —
S2 | search: memory-search(Hybrid: 70% Cosine+30% BM25, 0.55 threshold) + standard-search(task intent, lang, stack, repo) | S1✅ | relevant knowledge | —
S3 | retrieve: memory-detail for full content if pointer rows insufficient | S2✅ | hydrated entries | —
S4 | select: use ONLY highly relevant memories + standards | S3✅ | filtered knowledge | —
S5 | acknowledge: after code gen using memory → memory-acknowledge(used|irrelevant|contradictory) | code generated? | feedback | —

## FSM — Creation Policy

Entry=S0 → S1  Exit=stored
Guard: store ONLY if durable + affects future behavior; use supersedes for overrides

S0 | categorize: type + tech tags; NEVER store coordination state (claims, file ownership) as memory | is durable? | classified | —
S1 | store: memory-store(decisions/patterns) or standard-store(normative rules) or handoff-create(transfer ctx) | S0✅ | stored | —
