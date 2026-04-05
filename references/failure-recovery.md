# Failure Recovery

Use this reference when browsing or extraction does not work on the first attempt.

## Principle

Do not keep repeating the same failing method without learning from the result.
Every failure should change the next step.

## Common recovery moves

### 1. Search result is not enough
Problem:
- only snippets or vague summaries are available

Recovery:
- move to the first-party page
- do not conclude from snippets alone

### 2. `web_fetch` output looks incomplete
Problem:
- missing main body
- missing key metadata
- text is truncated or clearly not the rendered page the user cares about

Recovery:
- switch to `browser`
- inspect rendered UI directly

### 3. Browser page is dynamic or confusing
Problem:
- page state is unclear
- expected content is hidden behind tabs/cards/expansion

Recovery:
- snapshot again
- inspect current visible state before acting
- use user-visible navigation rather than guessing hidden structure

### 4. Current page is not the actual target
Problem:
- still on search results
- still on an intermediate landing page
- profile/post/question not yet opened

Recovery:
- do not summarize yet
- continue until the real target page is opened

### 5. Login is required
Problem:
- content is inaccessible without session state

Recovery:
- prefer existing logged-in browser state
- if unavailable, tell the user exactly what needs login
- resume after login rather than faking certainty

### 6. Evidence is only secondary
Problem:
- only media reports, reposts, or search summaries are available

Recovery:
- label it clearly as secondary evidence
- keep looking for first-party confirmation when verification matters

### 7. UI changed from prior assumptions
Problem:
- memorized route or old pattern no longer matches the page

Recovery:
- trust the current snapshot over old assumptions
- re-orient from the current visible UI
- update site-pattern guidance later if the new pattern proves stable
