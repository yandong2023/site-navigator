# Runtime Modes

Use this reference when deciding how browsing strategy changes between desktop and server environments.

## Desktop mode

Typical traits:
- host browser available
- possible access to an existing logged-in browser state
- better fit for dynamic social/content platforms

Preferred approach:
- use browser early when rendered state matters
- reuse existing browser state when login-dependent access matters
- prefer direct site navigation for platforms like Xiaohongshu, Zhihu, WeChat, and Bilibili

## Server mode

Typical traits:
- no user desktop session
- often relies on headless browser or lightweight fetch paths
- login state may be weaker or absent

Preferred approach:
- prefer direct URL access first
- use lightweight reading where possible
- switch to headless/browser-backed access when rendering matters
- be more cautious about login-dependent platforms and anti-bot sensitivity

## Rule

Routing should adapt not only to site type, but also to runtime type.
Desktop and server environments may need different “best” paths for the same target.
