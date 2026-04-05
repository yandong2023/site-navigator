---
domain: xiaohongshu.com
aliases: [xiaohongshu, xhs, 小红书]
updated: 2026-04-05
---

## Platform traits
- Public content is usually best handled in a real browser.
- Discovery is UI-first: cards, creators, post pages, search suggestions, and feed context.
- Rendered state matters for screenshots, visible metadata, and proof of what is currently shown.
- Publishing, creator tools, and account operations are sensitive and require explicit approval.

## Effective patterns

### Search / discovery
- Use `browser` rather than generic search as the default path.
- Open the site, snapshot the visible UI, then identify cards, creators, tabs, or search entry points.
- Navigate inside the site instead of relying on stale search snippets.

### Post inspection
- Once on a post page, capture the visible metadata the user actually cares about: title-like text, author/account, engagement indicators if visible, and the main content.
- Use screenshots only when visual proof matters.

### Account / creator inspection
- Stay browser-first.
- Confirm that the page is really the target creator before summarizing.
- Prefer stable, visible identifiers from the rendered page instead of inferred identity from external search results.

## Known pitfalls
- Search-engine snippets are often incomplete or detached from the actual rendered page.
- Static extraction may miss the page state or content ordering the user cares about.
- UI changes frequently; current snapshot state is more reliable than memorized assumptions.
