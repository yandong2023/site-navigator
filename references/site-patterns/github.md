---
domain: github.com
aliases: [github]
updated: 2026-04-05
---

## Platform traits
- GitHub has strong first-party structure for repos, releases, issues, PRs, commits, and docs.
- Many reading tasks can be solved without a browser; some rendered UI checks still benefit from browser inspection.

## Effective patterns
- Use official repo pages as source of truth.
- For README, docs, release notes, and changelog pages, try `web_fetch` first.
- Use `browser` for rendered UI state, Actions pages, tabbed views, or visual proof.
- Use native GitHub operations/CLI when the task is structured GitHub management rather than plain page reading.

## Known pitfalls
- Mirrors and reposted summaries are secondary sources.
- Screenshots show rendered state but are not substitutes for structured repo facts when those are directly available.
