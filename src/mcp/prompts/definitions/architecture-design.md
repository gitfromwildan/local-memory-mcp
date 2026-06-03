---
name: architecture-design
description: Plan system architecture, component layout, and data flow
arguments:
  - name: tech_stack
    description: Technology stack
    required: true
  - name: requirements
    description: Key requirements
    required: true
agent: System Architect
version: "1.0.0"
category: planning
tags: [architecture, system-design, components, data-flow, adr]
---

## FSM

Entry=S0 → S1 → S2 Exit=done
Guard: S(N) req S(N-1)✅

S0 | review tech_stack & requirements | — | component list, data flow map | —
S1 | design: component diagram(blocks+responsibilities) + data flow(information movement) + ADRs(rationale) + scalability/reliability(growth+failure) + security(identity,protection,boundaries) | S0✅ | design decisions | —
S2 | document artifacts | S1✅ | architecture docs | design/architecture/

## Chain

← N/A
→ architecture-documentation: design/architecture/ → as-built architecture doc
