---
domain: zhihu.com
aliases: [zhihu, 知乎]
updated: 2026-04-05
---

## Platform traits
- Many direct answer/article/question pages are readable, but ranking/order/context may still depend on rendered UI.
- User intent often targets the top answers, specific authors, or answer ordering rather than just raw text.

## Effective patterns
- Use direct question/article URLs when available.
- Use `web_fetch` for simple reading tasks.
- Use `browser` when answer ordering, profile navigation, or rendered context matters.

## Known pitfalls
- Static text alone may lose answer ranking context.
- Search snippets should not replace the actual answer page.
