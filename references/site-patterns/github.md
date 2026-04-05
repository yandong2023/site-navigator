---
domain: github.com
aliases: [github]
updated: 2026-04-05
---

## Platform traits
- GitHub has strong first-party structure for repos, commits, releases, issues, PRs, and docs.
- Many reading tasks can be solved with direct page reading or structured GitHub operations.
- Some rendered UI checks still benefit from browser inspection.

## Effective patterns

### Repo understanding
- README, docs, release notes, and changelog pages are often `web_fetch` first.
- Prefer official repo pages and official release pages over summaries from elsewhere.

### Issue / PR / release inspection
- If the task is mainly reading status, text, labels, timestamps, or changelog notes, direct first-party pages are usually enough.
- Use `browser` when rendered tabs, UI state, or current page layout matters.

### Interactive verification
- Use `browser` for Actions pages, rendered checks UI, tabbed interfaces, or visual confirmation tasks.
- Use structured GitHub operations when the task is more about data/state than page visuals.

## Known pitfalls
- Mirrors and reposted summaries are secondary sources.
- Screenshots show rendered state but should not replace direct repo facts when those are available from first-party sources.
