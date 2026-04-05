# Architecture Diagram Draft

Use this as the source text for a future visual diagram.

```text
User link / target
        |
        v
Route selection
(direct URL / platform-aware navigation / browser fallback)
        |
        v
Current page judgment
(discovery surface vs real target page)
        |
        +--------------------+
        |                    |
        v                    v
real target page        not target yet
        |                    |
        v                    v
source/evidence check   continue navigation / switch method
        |
        v
stable-first answer
        |
        v
optional enhancement
(screenshots / extra links / follow-up)
```
