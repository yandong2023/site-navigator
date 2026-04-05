---
name: site-navigator
description: OpenClaw-native web browsing, site navigation, logged-in page access, and source verification strategy. Use when the task involves visiting websites, reading pages, navigating dynamic or login-gated sites, extracting information from rendered UI, interacting with sites like GitHub, Zhihu, Xiaohongshu, and WeChat public content, or deciding between browser, web_fetch, direct page access, and parallel research. Prefer this skill for OpenClaw web tasks that should avoid Brave-based search and instead rely on direct site navigation, official sources, and browser-native access.
---

# site-navigator

Use OpenClaw's native tools first. Treat this skill as a **strategy layer**, not a sidecar browser stack.

Primary goals:
- reach the target page with the lightest reliable method
- prefer direct site navigation and first-party sources over search-engine snippets
- use real browser state when the site is dynamic or login-gated
- keep user-visible conclusions stable; do not expose noisy intermediate output as if it were final

## Supported target classes

This skill is especially useful for:
- **WeChat public content** (微信公众号 / articles reachable from shared links)
- **Xiaohongshu** (小红书 public pages, creator pages, posts, search/discovery via browser)
- **Zhihu** (知乎 articles, questions, answers, profiles)
- **GitHub** (repos, issues, PRs, changelogs, docs, code context)
- official docs and product sites
- dynamic web apps and dashboards

## Tool routing without Brave dependency

Do **not** assume Brave API search is the primary path.
Prefer these routes:

### Route A — Direct URL access
If the user already provides a URL, start with the URL.

- Use `web_fetch` for readable static pages.
- Use `browser` for dynamic, rendered, or login-gated pages.

### Route B — In-site navigation via browser
If the user names a site + target but no exact URL is given, prefer opening the site and navigating inside it with `browser` when that is more reliable than generic search.

Examples:
- “看一下这个知乎话题下的高赞回答”
- “去小红书搜某个账号”
- “看微信公众号这篇文章”

### Route C — Web search for discovery only
Use `web_search` only as a discovery layer when direct URL or in-site navigation is not enough.
After discovery, move to first-party pages quickly.

Never treat search snippets as final evidence when the task is verification.

## Core decision rule

Choose the **lightest reliable method**:

1. `web_fetch` for static readable content
2. `browser` for dynamic pages, rendered UI, login state, screenshots, clicks, scroll, or filters
3. `sessions_spawn` only for independent multi-target research

Do not introduce extra proxy stacks or curl-based browser control unless the user explicitly asks for an experiment.

## Stable-first browsing

For user-facing browsing tasks, separate output into:

### 1) Decision layer (must be stable)
Show only after you have enough evidence.
Examples:
- the answer to the user’s question
- the confirmed page state
- the final comparison summary
- the final identified source/article/repo/author/account

### 2) Enhancement layer (can be progressive)
Add afterward if helpful.
Examples:
- screenshots
- additional links
- extra metadata
- follow-up pages worth checking

Do not present a half-confirmed page state as if it were final.

## Browser workflow

When a real browser is needed:

1. `browser.open` or `browser.navigate`
2. `browser.snapshot` with `refs="aria"`
3. inspect the current page state before acting
4. use `browser.act` for click/type/fill/press
5. use `browser.screenshot` only when visual proof matters

Prefer `snapshot + act` over fragile assumptions.

## Logged-in browsing

Use browser state when:
- the site renders content only after login
- the target depends on cookies/session
- the useful path is only available through normal browsing

Guidelines:
- keep actions scoped to the task
- do not publish/post/send without explicit user permission
- do not modify account settings unless asked
- if login is missing and truly required, tell the user exactly what needs login

## Site-specific guidance

### WeChat public content
Prefer direct article URLs when available.

Use `web_fetch` first if the page content is readable.
If extraction is incomplete or the page is blocked/trimmed, switch to `browser`.

Typical tasks:
- read article content
- capture title/author/date
- summarize an article
- verify whether a linked article still exists

### Xiaohongshu
Treat Xiaohongshu as a **browser-first** target in most cases.

Use browser when the task requires:
- search/discovery
- viewing creator pages
- navigating feeds/cards
- checking rendered post content
- collecting screenshots as proof

Avoid relying on generic search snippets as the final source of truth.

### Zhihu
Use `web_fetch` for direct question/article URLs when content is extractable.
Switch to `browser` when:
- content is partially rendered
- the useful answer ordering depends on the live page
- profile/question navigation matters

### GitHub
Prefer the lightest path that fits the task:
- direct repo metadata or issue/PR state: use native GitHub flows or `gh` when appropriate
- README/docs/changelog pages: `web_fetch` is often enough
- rendered UI state, Actions pages, or interactive inspection: `browser`

Always prefer official repo pages over third-party mirrors when verifying facts.

## First-party source hierarchy

When verifying facts, prefer:
1. official page / original URL
2. official repo or official docs
3. directly rendered UI evidence
4. reputable secondary report only if first-party evidence is unavailable

State uncertainty clearly when only secondary sources exist.

## Parallel research

Use `sessions_spawn` only when targets are independent.
Good cases:
- compare multiple products/sites
- inspect several official sources in parallel
- gather comparable facts from multiple pages

Bad cases:
- one continuous browser session
- one task that depends on the previous click/result

## Site patterns

When repeated work reveals stable domain knowledge, store it in:
- `references/site-patterns/<domain>.md`

Record only validated facts:
- whether the site is browser-first or fetch-first
- common entry points
- known extraction failures
- login requirements
- UI patterns worth remembering

Do not store secrets, cookies, tokens, or personal data.

## References

Read domain files when relevant:
- `references/site-patterns/wechat.md`
- `references/site-patterns/xiaohongshu.md`
- `references/site-patterns/zhihu.md`
- `references/site-patterns/github.md`

## Anti-patterns

Avoid:
- treating search snippets as verification
- overusing generic search when a direct site path exists
- exposing unstable intermediate findings as final
- browser automation for pages that `web_fetch` can already solve cleanly
- parallelizing a single tightly coupled browsing flow
