# OpenClaw Browser Playbook

Use this reference when a task needs real browser interaction inside OpenClaw.

## Default browser flow

1. Open or navigate to the page.
2. Take a snapshot with `refs="aria"`.
3. Inspect the current visible state.
4. Choose the next action based on what is actually visible.
5. Act with click/type/fill/press.
6. Re-snapshot after meaningful state changes.
7. Take screenshots only when they provide evidence or visual confirmation the user cares about.

## Prefer `refs="aria"`

Use `browser.snapshot` with `refs="aria"` whenever the task involves multiple interactions.
This gives more stable references across steps than role-name matching alone.

## When browser is better than web_fetch

Prefer `browser` when:
- the content is partially rendered or delayed
- the useful data depends on tabs, filters, dialogs, or scroll
- visual layout is part of the question
- login state matters
- the user says “go to this site and check” rather than just “read this article”

## When web_fetch is better than browser

Prefer `web_fetch` when:
- the URL is known
- the page is mainly article/doc text
- no interaction is needed
- you only need content extraction or summarization

## Stable-first rule

Do not expose a changing intermediate browser conclusion as the final answer.

Bad pattern:
- report a conclusion after only the first visible partial state
- keep revising the main answer while still discovering the page

Better pattern:
- inspect enough of the page to form a stable answer
- then answer
- then add optional screenshots or extra findings

## Screenshot rules

Take screenshots when:
- the user asks for proof
- the page rendering itself matters
- a bug or UI state must be documented
- before/after comparison matters

Do not take screenshots by default when extracted text is enough.

## Interaction rules

- snapshot before acting on an unfamiliar page
- use the same tab target for a continuous flow
- avoid unnecessary tab churn
- do not assume selectors or page structure without checking the snapshot
- prefer explicit user-visible navigation over hidden assumptions

## Login-dependent tasks

When the page needs login:
- prefer the existing logged-in browser state
- avoid asking for credentials if the browser session already has access
- if login is missing, tell the user exactly what needs login

## Parallel browsing

Only parallelize when targets are independent.
Do not split one sequential click flow across multiple agents.
