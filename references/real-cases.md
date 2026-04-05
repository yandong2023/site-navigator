# Real Cases

These are representative cases that show why `site-navigator` exists.

## Case 1 — WeChat article link
Problem:
- user sends a real WeChat article link
- generic search is unnecessary
- the real need is to open the article page and read the actual content

Skill value:
- start from the real link
- verify that the article page is accessible
- summarize from the real page, not from secondary snippets

## Case 2 — Zhihu article link
Problem:
- user sends a Zhihu article URL
- the task is not “search around Zhihu”
- the task is “confirm whether this is the real page and read it”

Skill value:
- direct open first
- determine whether the page is the real article page
- summarize only after target-page judgment is stable

## Case 3 — GitHub repo page without wasting paid search
Problem:
- user already knows the repo page or exact target
- paid search adds cost and indirection

Skill value:
- open the first-party repo page directly
- inspect the actual repo UI/content
- avoid unnecessary paid-search dependency for a task that is already target-known
