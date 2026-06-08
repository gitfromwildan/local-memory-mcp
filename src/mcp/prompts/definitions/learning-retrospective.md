---
name: learning-retrospective
description: Harvest knowledge from completed work.
arguments:
  - name: task_id
    description: ID of completed task.
    required: false
agent: Knowledge Harvester
category: workflows
version: "1.0.0"
tags: [workflow, retrospective, memory, knowledge-management]
---

## Learning Retrospective

Entry=S0 → S1  Exit=stored
Guard: S(N) req S(N-1)✅

S0 | identify: mistakes (bugs/quirks), decisions (trade-offs/pivots), patterns (conventions) | task_id? | knowledge items | —
S1 | store via memory-store (type=mistake|decision|pattern, include tech tags, concise) | S0✅ | durable memories | —

Task: {{task_id}}
