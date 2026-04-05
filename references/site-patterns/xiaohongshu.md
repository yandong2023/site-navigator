---
domain: xiaohongshu.com
aliases: [xiaohongshu, xhs, 小红书]
updated: 2026-04-05
---

## Platform traits
- Public content is usually better handled in a real browser than in static extraction.
- Discovery flows are UI-first: cards, creators, feeds, and post pages.
- Rendered state matters for screenshots, visible post metadata, and proof of what is currently shown.
- Tasks around publishing, creator tools, or account operations are high-risk and require explicit user approval.

## Effective patterns
- Treat Xiaohongshu as browser-first for search and discovery.
- Open the site in `browser`, take a snapshot, and identify the current visible navigation path before clicking.
- Use screenshots only when they are meaningful evidence, not as default output.
- For “find this account / post / topic” tasks, navigate within the site rather than relying on generic search snippets.

## Known pitfalls
- Generic search results may be incomplete, stale, or detached from the actual rendered page.
- Static extraction often misses the real page state or the content ordering the user cares about.
- UI can change, so rely on current snapshots rather than memorized selectors.
