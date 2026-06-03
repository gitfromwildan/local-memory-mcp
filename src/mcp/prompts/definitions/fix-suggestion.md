---
name: fix-suggestion
description: Targeted fix with before/after code and test case.
arguments:
  - name: tech_stack
    description: Target tech stack.
    required: true
  - name: bug_description
    description: Bug behavior.
    required: true
  - name: root_cause
    description: Identified root cause.
    required: true
agent: Debugging Expert
version: "1.1.0"
category: debugging
tags: [fix, patch, bug-fix, code-change, test-case, debugging]
---

## FSM

Entry=S0 → S1 Exit=suggestion
Guard: S(N) req S(N-1)✅

S0 | analyze inputs (tech_stack, bug_description, root_cause) | all req provided? | diagnosis | —
S1 | produce: explanation + before/after diff(`diff ... `) + meta checklist + regression test | S0✅ | fix suggestion | —

## Output Format (S1)

- Explanation: Why bug happens + how fix works (prose)
- Before/After: `diff blocks` with line comments
- Meta checklist: config changes, migrations, dependencies
- Verification: regression test case (code block)

## I/O

tech_stack + bug_description + root_cause → diagnosis report + fix suggestion
