---
name: export-task-to-github
description: Export local tasks to GitHub Issues
arguments:
  - name: owner
    description: GitHub repo owner (hint: run `git remote -v` to extract from origin URL)
    required: true
  - name: repo
    description: GitHub repo name (hint: run `git remote -v` to extract from origin URL)
    required: true
  - name: task_id
    description: Local task ID
    required: true
agent: Integration Architect
category: workflows
version: "1.0.0"
tags: [workflow, github, task-sync, mcp]
---

## FSM

Entry=S0 → S1 → G1 → S2 → S3 → S4 Exit=exported|skipped
Guard: S(N) req S(N-1)✅; MCP + GitHub tools ONLY

S0 | fetch task via task-detail | task_id exists? | task data | —
S1 | sync check via search_issues for task_code | S0✅ | existing issue? | —
G1 | dedup gate — if exists→update local task metadata with URL, DO NOT re-create | S1✅ | exists→skip+link / new→S2 | —
S2 | create issue via issue_write (match title/body, append task_code+id) | G1→new | GitHub issue created | —
S3 | post comments via add_issue_comment | S2✅ | comments transferred | —
S4 | link: task-update with GitHub URL + comment | S3✅ | task updated | —
