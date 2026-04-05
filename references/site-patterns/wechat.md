---
domain: mp.weixin.qq.com
aliases: [wechat, weixin, 微信公众号]
updated: 2026-04-05
---

## Platform traits
- Public article URLs are often directly shareable.
- Some article content is readable as a normal page; some extraction layers may miss formatting or embedded media.
- Verification tasks usually care about title, author, publication date, article body, and whether the article still resolves.

## Effective patterns
- Start from the exact article URL if available.
- Try `web_fetch` first for article reading/summarization.
- Switch to `browser` if the extracted content looks incomplete or if visual/page-state confirmation matters.

## Known pitfalls
- Search-engine snippets are not the article.
- Embedded media, formatting, or secondary linked content may require browser inspection.
