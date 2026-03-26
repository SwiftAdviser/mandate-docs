# QA Report: Block Reasons

**File:** `/reference/block-reasons.mdx`
**Date:** 2026-03-26
**Status:** PASS

## Checklist

| # | Rule | Pass |
|---|------|------|
| 1 | Frontmatter: title, sidebarTitle, description | YES |
| 2 | No em dashes (U+2014) | YES |
| 3 | No filler words | YES |
| 4 | Short paragraphs (2-4 sentences) | YES |
| 5 | "Next Steps" CardGroup at bottom | YES |
| 6 | 3-5 cross-links | YES (3 cards) |
| 7 | Correct terminology | YES |
| 8 | Tables complete and scannable | YES |

## Findings

No violations found. Page is clean.

- Line 9: Opening paragraph answers "What is a block reason?" in under 60 words. Good GEO compliance.
- Line 26: "14 sequential checks" matches the writing guide's specific numbers rule.
- Lines 32-75: Tables split by category (security, schedule/allowlist, spend, raw, risk/reason) with 4 columns each: blockReason, HTTP, Cause, Resolution. Every documented blockReason has a resolution. 14 block reasons total.
- Lines 77-99: Code example shows imports, realistic variable names, and error paths. Good.
- Lines 102-104: Warning callout about not suppressing blocks. Appropriate.
- Lines 106-118: Next Steps with 3 cards linking to /sdk/errors, /guides/handle-errors, /troubleshooting/common-errors.

## Developer Experience Notes

Strong. A developer receiving `per_tx_limit_exceeded` can Cmd+F the string and immediately find: what HTTP code it returns (422), why it fires (amount exceeds spend_limit_per_tx_usd), and how to fix it (reduce amount or raise the limit). The category grouping (Security, Schedule/Allowlist, Spend, Raw, Risk/Reason) mirrors the policy engine evaluation order, which helps devs understand *when* each check runs.

One minor DX suggestion: consider adding an anchor link per blockReason value (e.g., `#per_tx_limit_exceeded`) so error handling code can deep-link directly. Currently the user must scroll within the category.

The code example at line 77 is a strong pattern: it shows the class hierarchy (CircuitBreakerError > RiskBlockedError > PolicyBlockedError) which maps directly to the table's HTTP status grouping.

## Score

**9/10**
