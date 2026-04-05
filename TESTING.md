# v0.7 Testing Notes

Goal: run a few realistic tasks against the skill design and refine based on real friction.

## Initial observations

### 1. `web_fetch` limitations in current OpenClaw environment
Attempting to fetch GitHub via `web_fetch` returned:
- `Blocked: resolves to private/internal/special-use IP address`

Implication:
- skill guidance should not over-presume that `web_fetch` is always available for every public site in the current runtime
- add a fallback note: if `web_fetch` is blocked or incomplete, move quickly to `browser` or another first-party path

### 2. Browser session volatility
A browser open to Zhihu returned a targetId, but immediate snapshot failed with `tab not found`.

Implication:
- skill should include a lightweight recovery rule for browser target loss / stale tab references
- re-open or re-snapshot should be treated as a normal recovery move, not an exceptional case

## Refinements to make
1. Add a note that OpenClaw runtime/network policy may restrict some `web_fetch` targets.
2. Add browser-target-loss recovery guidance.
3. Clarify that tool choice is not just page type, but also runtime/tool availability.
