---
name: csl-scrapper
description: Scrape trusted documentation from a URL into atomic CSL coding standards entries.
arguments:
  - name: source_url
    description: Canonical URL for the documentation source to scrape.
    required: true
agent: Documentation Scraper
category: workflows
version: "1.0.0"
tags: [workflow, csl, scraping, coding-standards, mcp]
---

## FSM

Entry=G0 → S0 → G1 → S1 → S2 → S3 → S4  Exit=stored|refused
Guard: S(N) req S(N-1)✅

G0 | source_url provided? | source_url arg exists? | → S0 / refuse | —
S0 | fetch via web_fetch | G0✅ | raw doc | —
G1 | content reachable + normative? | S0✅ | → S1 / refuse | —
S1 | extract atomic rules: 1 entry=1 rule, keep code examples, detect nav menus for sub-pages, ignore marketing/release notes, preserve source meaning | S0✅ | atomic entries, sub-page URLs | —
S2 | dedup via standard-search (skip if high-confidence match; update if new source more authoritative) | S1✅ | filtered entries | —
S3 | store via standard-store: parent first→children with parent_id; context=topic area; version=1.0.0(default); is_global=true(unless repo-specific); metadata={source_url, evidence_excerpt} | S2✅ | CSL entries stored | —
S4 | create scrape tasks for each sub-page URL via task-create | sub-page URLs exist? | MCP tasks queued | —

Source: {{source_url}} Repo: {{current_repo}}
