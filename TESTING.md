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


## Second-round trial notes (v0.8)

### Focus areas
- GitHub first-party page reading under current runtime constraints
- browser-first platform navigation assumptions
- direct-target vs discovery-page distinction

### Working hypotheses
1. The skill should more strongly distinguish between “I have reached the real target page” and “I am still on a discovery surface”.
2. For platform tasks, the biggest risk is summarizing too early from search/discovery UI.
3. Runtime-aware fallback should be considered a first-class routing dimension, not just a recovery note.


### GitHub browser trial
Result:
- GitHub repo page was reachable with `browser`.
- Snapshot confirmed a stable first-party page state with repo name, tabs, file list, and README visible.

Takeaway:
- In the current runtime, GitHub is a strong example of “browser can serve as the reliable fallback when `web_fetch` is blocked”.
- The skill should more strongly encode the distinction between:
  1. discovery surface
  2. actual target page
- For GitHub, once the repo page itself is open, the answer can often be considered stable enough to summarize.

### New refinement theme
The skill should explicitly teach: **do not summarize from discovery surfaces when the task requires the real target page**.
This is especially important for Xiaohongshu, Zhihu, and search-heavy platform tasks.
