---
domain: github.com
aliases: [github]
updated: 2026-04-05
---

## Platform traits
- GitHub has strong first-party structure for repos, issues, PRs, releases, commits, and Actions.
- Some tasks are better served by native GitHub APIs/CLI; others are fine with page reading.

## Effective patterns
- Use official repo pages as the source of truth.
- For README, docs, changelog, and release notes, `web_fetch` is often enough.
- For rendered UI, Actions pages, or interactive verification, use `browser`.
- For structured GitHub operations, consider the dedicated GitHub skill/CLI path when available.

## Known pitfalls
- Third-party mirrors or scraped summaries are secondary sources.
- UI screenshots are evidence of current rendered state, not substitutes for source data when structured repo metadata is available.
