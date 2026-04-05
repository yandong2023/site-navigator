# Task Patterns

Use this reference to quickly choose a browsing approach based on the user's task shape.

## 1. Read one known page

Examples:
- “读一下这篇文章”
- “看这个 GitHub release note”
- “总结这个知乎回答”

Preferred path:
1. use the exact URL
2. try `web_fetch` first
3. switch to `browser` only if rendered state, login, or visual inspection matters

## 2. Verify whether a page/post/account exists

Examples:
- “这个公众号文章还在吗？”
- “这个小红书账号是真实存在的吗？”
- “这个 GitHub repo 还在更新吗？”

Preferred path:
1. direct URL if available
2. official site first
3. use `browser` if current rendered state is important
4. only conclude after checking the real target page, not just snippets

## 3. Find something within a platform

Examples:
- “去小红书找这个博主”
- “看看知乎上有没有这个问题”
- “看看 GitHub 有没有这个项目”

Preferred path:
1. browser-first if the platform is navigation-heavy
2. use in-site navigation to reach the actual target page
3. only summarize after opening the real target, not just search results

## 4. Compare multiple official sources

Examples:
- “比较这几个官网首页怎么写”
- “看看三个产品的 pricing 页面区别”
- “对比几个仓库最近更新”

Preferred path:
1. gather first-party pages
2. use parallelism only if targets are independent
3. produce a stable comparison summary first
4. attach evidence/links/screenshots second

## 5. Inspect dynamic or login-gated state

Examples:
- “登录后这个页面显示什么？”
- “这个后台是否有导出按钮？”
- “这个站里能不能筛选到某个结果？”

Preferred path:
1. browser-only
2. snapshot the current state
3. act based on the visible UI
4. re-snapshot after state changes
5. report only once the page state is stable enough to trust

## 6. Reproduce or document a UI issue

Examples:
- “这个页面是不是加载错了？”
- “验证一下这里有没有跳闪/重排”
- “帮我截图证明这个按钮在不在”

Preferred path:
1. browser
2. inspect current state
3. capture evidence screenshots only where useful
4. describe exact visible behavior, not guesses
