# site-navigator

OpenClaw-native web browsing and site navigation skill.

`site-navigator` is a strategy-first skill for web tasks in OpenClaw. It is designed for tasks that require:
- visiting websites directly
- navigating within platforms instead of relying on generic search snippets
- inspecting rendered UI with the browser tool
- handling login-gated or dynamic pages
- keeping conclusions stable before reporting them to the user

It is especially useful for:
- WeChat public content
- Xiaohongshu
- Zhihu
- GitHub
- official product sites and docs
- dynamic pages that are better handled with OpenClaw browser automation

## Design goals

- Prefer direct site access over search-engine dependency
- Prefer first-party evidence over secondary summaries
- Use OpenClaw native tools (`browser`, `web_fetch`, `web_search`, `sessions_spawn`)
- Separate stable conclusions from progressive enhancement

## Repository structure

- `SKILL.md` — main skill definition
- `references/openclaw-browser-playbook.md` — browser operating patterns
- `references/output-contract.md` — how to present browsing results
- `references/source-hierarchy.md` — evidence strength model
- `references/task-patterns.md` — common web task shapes
- `references/failure-recovery.md` — fallback and route-changing guidance
- `references/examples.md` — concrete usage examples
- `references/site-patterns/*.md` — domain-specific notes

## Status

Early version, intended for iterative refinement inside OpenClaw workflows.

## Roadmap

- Validate against more real OpenClaw browsing tasks
- Expand site patterns based on repeated use
- Refine trigger boundaries and reporting rules
- Prepare for broader public iteration
