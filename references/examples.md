# Examples

Use these examples as pattern references, not rigid scripts.

## Example 1 — Verify a WeChat article

User asks:
- “这篇公众号文章还在吗？顺便帮我总结一下”

Preferred approach:
1. start from the exact article URL
2. try `web_fetch` first
3. if extraction is incomplete or the page state matters, switch to `browser`
4. confirm the article exists before summarizing
5. report: existence status first, summary second, screenshot only if useful

## Example 2 — Find a Xiaohongshu creator

User asks:
- “去小红书找一下这个账号，看是不是官方号”

Preferred approach:
1. use `browser`
2. navigate inside Xiaohongshu rather than stopping at search-engine discovery
3. open the actual creator page
4. verify using visible profile identifiers from the rendered page
5. answer only after opening the real target page, not from search results alone

## Example 3 — Check a Zhihu question’s top answer

User asks:
- “看看知乎这个问题下面高赞回答在说什么”

Preferred approach:
1. direct question URL if available
2. use `browser` if ranking/order matters
3. inspect the visible answer ordering
4. summarize the top visible answer(s)
5. make it explicit if only part of the answer list was inspected

## Example 4 — Verify a GitHub repo update

User asks:
- “这个 GitHub 仓库最近还在更新吗？”

Preferred approach:
1. go to the official repo page
2. inspect commits / releases / recent activity from first-party pages
3. prefer direct repo evidence over third-party summaries
4. report a stable answer with dates or page evidence

## Example 5 — Compare several official product pages

User asks:
- “对比这三个官网首页怎么描述自己”

Preferred approach:
1. collect the three official pages
2. use `web_fetch` where possible
3. use browser only if rendered state matters
4. summarize the comparison first
5. add links and screenshots second
