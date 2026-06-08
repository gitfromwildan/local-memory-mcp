---
name: tech-affinity-scout
description: Scout best practices from similar tech projects.
arguments:
  - name: tags
    description: CSV tech tags (e.g., 'react, tailwind').
    required: true
agent: Tech Scout
category: planning
version: "1.0.0"
tags: [planning, patterns, memory, tech-affinity]
---

## Tech Affinity Scout

Entry=S0 → S1 → S2 → S3 → S4 Exit=scouted
Guard: S(N) req S(N-1)✅

S0 | search: memory-search (current_tags=[tags]) + standard-search (stack=[tags]) + web_search (current practices for stack) | tags provided? | pointer rows + web results | —
S1 | hydrate: memory-detail for relevant pointers | S0✅ | full entries | —
S2 | filter: pattern + decision + coding standard + web_search entries from similar stacks | S1✅ | applicable knowledge | —
S3 | adapt: explain adaptation to current project; separate memory-derived vs standards vs web_search | S2✅ | adaptation guide | —
S4 | verify: confirm all relevant patterns evaluated, adaptation guidance is actionable | S3✅ | verified | —

Tags: {{tags}}

## Delegation

Web search MUST be delegated to a coding subagent (general/explore). Main agent must NOT execute web_search directly.
