---
name: csl-from-docs
description: Create atomic CSL coding standards entries from a local file or directory path.
arguments:
  - name: path
    description: Local path (file or directory) containing documentation or standards.
    required: true
agent: Documentation Processor
category: workflows
version: "1.0.0"
tags: [workflow, csl, coding-standards, documentation, mcp]
---

## CSL from Docs

Entry=G0 → S0 → S1 → S2 → S3 → S4  Exit=stored|refused
Guard: S(N) req S(N-1)✅

G0 | path exists + readable + normative? | path provided? | → S0 / refuse | —
S0 | discover: if dir→list_directory then read_file each; if file→read_file | G0✅ | raw content | —
S1 | extract atomic rules: 1 entry=1 rule, keep code examples, split bundled, preserve source meaning, ignore boilerplate | S0✅ | atomic entries | —
S2 | dedup via standard-search (skip if high-confidence match; update if new source more authoritative) | S1✅ | filtered entries | —
S3 | store via standard-store: parent first→children with parent_id; context=topic area; version=1.0.0(default); is_global=true(unless repo-specific); metadata={original_path, evidence_excerpt} | S2✅ | CSL entries stored | —
S4 | verify: confirm stored count matches extracted, validate parent/child linkage, check metadata provenance | S3✅ | verified | —

Path: {{path}} Repo: {{current_repo}}
