---
name: memory-guided-review
description: Review code for compliance with stored decisions.
arguments:
  - name: file_path
    description: File to review.
    required: true
agent: Code Auditor
category: coding
version: "1.0.0"
tags: [code-review, memory, compliance, mcp]
---

## Memory Guided Review

Entry=S0 → S1 → S2 → S3  Exit=reviewed
Guard: S(N) req S(N-1)✅

S0 | search: memory-search (file_path) + standard-search (lang, stack, repo) | file_path provided? | relevant rules | —
S1 | hydrate: memory-detail for relevant pointers | S0✅ | full rules | —
S2 | evaluate compliance vs patterns, documented mistakes, standards | S1✅ | violation list | —
S3 | feedback: suggest fixes citing source (memory|standard) | S2✅ | review report | —

File: {{file_path}}
