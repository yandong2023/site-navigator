# Source Hierarchy

Use this reference when deciding which web evidence is strong enough to support a conclusion.

## Tier 1 — First-party source

Strongest evidence.
Examples:
- official website page
- official product docs
- official repo, release page, PR, issue, or changelog
- original article URL on the source platform
- directly rendered UI state from the official page

Use Tier 1 whenever possible.

## Tier 2 — Structured first-party adjacent evidence

Still strong, but slightly more indirect.
Examples:
- official API/CLI output reflecting first-party state
- exported data from an official system
- cached but clearly first-party-hosted mirrors inside the same product ecosystem

Use when the direct page is awkward but the source is still clearly first-party.

## Tier 3 — Reputable secondary source

Useful when first-party material is unavailable.
Examples:
- reputable media report
- reputable analyst or documentation site summarizing official information
- trustworthy third-party page linking clearly back to the original source

When using Tier 3, say explicitly that it is secondary evidence.

## Tier 4 — Discovery-only evidence

Do not treat this as final verification by itself.
Examples:
- search-engine snippets
- aggregator summaries
- reposts with no reliable source chain
- social reposts of unclear origin

Use Tier 4 only to discover where to investigate next.

## Rule of use

For verification tasks:
- prefer Tier 1
- fall back to Tier 2 when practical
- use Tier 3 only with explicit labeling
- never stop at Tier 4 if the task asks for confirmation or verification

## Reporting rule

When evidence is not Tier 1, make that visible in the answer.
Examples:
- “我看到的是 GitHub 官方 release 页面，属于一手来源。”
- “目前只找到媒体转述，没看到官方原文，因此这里只能作为二手依据。”
- “现在只有搜索摘要，还不能算确认。”
