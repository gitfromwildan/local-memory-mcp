---
name: security-triage
description: Assess vulnerability exploitability and prioritize fix.
arguments:
  - name: tech_stack
    description: App stack.
    required: true
  - name: vulnerability_report
    description: Report details (CVE, SAST).
    required: true
  - name: codebase_context
    description: Usage context.
    required: false
agent: Security Engineer
category: debugging
version: "1.0.0"
tags: [security, triage, vulnerability, cvss, appsec]
---

## Security Triage

Entry=S0 → S1 → S2 → S3 → S4 → S5 Exit=assessment
Guard: S(N) req S(N-1)✅

S0 | classify: web_search (CVE/CVSS details) → type, CVE, CVSS vector, score | tech_stack + vuln_report provided? | classification | —
S1 | assess exploitability: reachability + attack scenarios | S0✅ | exploit scenarios | —
S2 | assess impact: CIA triad | S1✅ | impact assessment | —
S3 | remediate: priority P0-P3 + fix steps | S2✅ | remediation plan | —
S4 | verify: testing method to confirm fix | S3✅ | verification plan | —
S5 | verify: confirm remediation addresses all exploit scenarios, verification plan is actionable | S4✅ | verified | —

Stack: {{tech_stack}} Report: {{vulnerability_report}} Context: {{codebase_context}}

## Delegation

Web search MUST be delegated to a coding subagent (general/explore). Main agent must NOT execute web_search directly.
