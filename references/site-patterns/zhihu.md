---
domain: zhihu.com
aliases: [zhihu, 知乎]
updated: 2026-04-05
---

## Platform traits
- Some article and question pages are readable directly, but ranking/order/context may matter as much as raw text.
- User intent often targets top answers, specific answerers, or visible answer ordering.

## Effective patterns
- If the exact question/article URL is known, try `web_fetch` first.
- Move to `browser` when answer ordering, profile context, or rendered interactions matter.
- Use direct page evidence instead of search snippets when the question is about what Zhihu currently shows.

## Known pitfalls
- Static text can lose ranking context.
- Search snippets do not preserve the on-page answer structure users usually care about.
