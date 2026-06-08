---
name: senior-code-review
description: Comprehensive production-readiness evaluation.
arguments:
  - name: tech_stack
    description: Tech stack.
    required: true
  - name: context
    description: Production context (SLA, data, conventions).
    required: false
agent: Principal Reviewer
version: "1.2.0"
category: coding
tags: [code-review, production-readiness, security, observability, senior-review, architecture]
---

## Senior Code Review

Entry=S0 → S1 → S2 → S3  Exit=decision
Guard: S(N) req S(N-1)✅; cite code evidence only; ONE fix option per finding

S0 | audit 6 dimensions: errors, security, performance (N+1, cache, complexity), observability (logs, metrics, traces), testing (coverage, quality), docs (clarity) | tech_stack provided? | findings[] | —
S1 | check cross-domain invariants: lifecycle, concurrency guard, derived state, upload safety, file>500→refactor, doc hierarchy | S0✅ | invariant results | —
S2 | assign severity: CRITICAL (bug/data loss) | HIGH (concurrency/arch) | MEDIUM (maintainability) | LOW (cosmetic) | S0-1✅ | scored findings | —
S3 | produce: DECISION (APPROVE|REQUEST_CHANGES|NOT_READY) + SEVERITY_SCORE + MESSAGE (blockers only) | S2✅ | review decision | —

Stack: {{tech_stack}} Context: {{context}}
