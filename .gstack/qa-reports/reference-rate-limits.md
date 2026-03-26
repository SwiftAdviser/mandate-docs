# QA Report: Rate Limits

**File:** `/reference/rate-limits.mdx`
**Date:** 2026-03-26
**Status:** PASS (minor)

## Checklist

| # | Rule | Pass |
|---|------|------|
| 1 | Frontmatter: title, sidebarTitle, description | YES |
| 2 | No em dashes (U+2014) | YES |
| 3 | No filler words | YES |
| 4 | Short paragraphs (2-4 sentences) | YES |
| 5 | "Next Steps" CardGroup at bottom | YES |
| 6 | 3-5 cross-links | PARTIAL (2 cards) |
| 7 | Correct terminology | YES |
| 8 | Tables complete and scannable | YES |

## Findings

- **Line 72: Only 2 Next Steps cards.** Links to /reference/error-codes and /api-reference/overview. Needs at least one more. Candidates: /sdk/mandate-client (SDK retry utilities), /guides/handle-errors, or /reference/block-reasons.

Everything else is clean:

- Line 4: Description is concise: "Rate limiting behavior, response headers, and retry strategies."
- Line 9: Opening paragraph answers "how rate limiting works" in 3 sentences. Key info: per-agent, per runtime key, returns 429 with Retry-After header.
- Lines 13-19: Default limits table. 5 endpoint categories with Rate Limit and Window columns. Clear numbers: 60/min for validation, 120/min for polling, 30/min for events, 10/min for registration, 120/min for dashboard.
- Lines 25-31: Response headers table. 3 headers documented.
- Lines 33-39: 429 response format with JSON example.
- Lines 44-61: Retry strategy with TypeScript code example. Shows exponential backoff (1s, 2s, 4s). Realistic implementation.
- Lines 64-66: Warning about tight polling loops. References SDK methods with their intervals (5s and 3s).
- Lines 68-70: Tip about custom rate limits for high-volume use.

## Developer Experience Notes

Good. The default limits table at line 13 is the primary lookup. A developer hitting 429s on `/validate` can immediately see the limit is 60/min. The retry code example at line 48 is copy-paste ready.

The Warning at line 64 about not polling in tight loops is well-placed. It names the SDK methods (`waitForApproval`, `waitForConfirmation`) and their intervals, giving developers the right tool instead of just telling them what not to do.

One suggestion: the page does not mention what happens to burst requests. If an agent sends 61 requests in the first second of a minute window, does the 61st get 429'd immediately, or is there any burst allowance? This level of detail helps developers design their request patterns. Not a blocker, but would improve the page.

The 2-card Next Steps is the only structural gap.

## Score

**8/10**
