---
name: root-cause-analysis
description: 5-Why analysis to trace bug origins.
arguments:
  - name: tech_stack
    description: Target tech stack.
    required: true
  - name: bug_description
    description: Bug behavior.
    required: true
  - name: symptoms
    description: Logs, errors, metrics.
    required: false
agent: Diagnostic Lead
category: debugging
version: "1.0.0"
tags: [root-cause, 5-why, debugging, diagnosis]
---

## Root Cause Analysis

Entry=S0 → S1 → S2 → S3  Exit=diagnosis
Guard: S(N) req S(N-1)✅

S0 | restate symptom: technical problem statement | tech_stack + bug_description provided? | symptom statement | —
S1 | 5-why analysis: causal chain from symptom to core failure | S0✅ | causal chain | —
S2 | identify root cause: "root cause is [X] because [Y], allowing [Z]" | S1✅ | root cause | —
S3 | recommend fix addressing root cause + prevention (monitoring/test) | S2✅ | recommendation | —

Stack: {{tech_stack}} Bug: {{bug_description}} Symptoms: {{symptoms}}
