# QA Report: troubleshooting/common-errors.mdx

**Reviewed:** 2026-03-26
**Reviewer:** Claude Opus 4.6 (doc QA agent)

---

## Checklist

| # | Rule | Pass? | Notes |
|---|------|-------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS | All three present. Description is action-oriented. |
| 2 | No em dashes (U+2014) | PASS | None found. |
| 3 | No filler words | PASS | None found. |
| 4 | Short paragraphs (2-4 sentences) | PASS | All paragraphs are within limit. |
| 5 | "Next Steps" CardGroup at bottom | PASS | Present, 3 cards. |
| 6 | 3-5 cross-links | PASS | 5 links: /troubleshooting/circuit-breaker-tripped (line 52), /dashboard/policy-builder (lines 60, 80), /sdk/errors (line 170), /reference/block-reasons (line 173), /guides/handle-errors (line 176). |
| 7 | Terminology | PASS | Uses "runtime key", "policy engine", "block reason", "circuit breaker", "dashboard" consistently. |
| 8 | Troubleshooting: exact errors, step-by-step, cause-solution mapping | PARTIAL | See findings. |

---

## Findings

### Line 7: Error format inconsistency
The section headings use a mix of formats: "401 Unauthorized: Invalid runtime key" (line 7), "403 Circuit breaker active" (line 28), "422 per_tx_limit_exceeded" (line 56), "202 Approval required" (line 119). Some use human-readable labels, others use the raw `blockReason` code. A consistent format like `<HTTP status> <blockReason code>: <human label>` would help agents pattern-match against errors programmatically.

### Line 106-116: Intent hash mismatch section is a redirect
The `intent_hash_mismatch` entry (lines 106-116) provides 4 quick fixes then links to the dedicated page. This is good for triage, but the 4 fixes lack code examples unlike every other section. Minor inconsistency.

### Line 145-165: Network error section missing HTTP status
Every other section starts with an HTTP status code. "Network error: API unreachable" has no status because it's a client-side error. This is correct, but adding a note like "(no HTTP response)" would make the pattern explicit for programmatic consumers.

### Line 155: Error code detection is Node.js specific
The error codes `ECONNREFUSED`, `ENOTFOUND`, `ETIMEDOUT` are Node.js system error codes. No mention of how to detect this in Python or other runtimes. The page shows only TypeScript examples, which is acceptable per the writing guide (TypeScript first), but a brief note about other runtimes would improve coverage.

### Line 157-158: Retry logic is comment-only
Lines 157-158 describe retry behavior in comments but do not show the actual retry implementation. An agent hitting this code gets a pattern with TODO-style comments rather than working code.

### Lines 167-179: Next Steps has 3 cards
The writing guide says 3-5 cross-links. Three cards is the minimum. Consider adding a card for /troubleshooting/intent-hash-mismatch (since it's a common error) and /guides/fail-safe (since network errors reference fail-safe behavior).

---

## Developer Experience Notes

**Scenario: AI agent gets a 422 with `blockReason: "per_tx_limit_exceeded"`.**

1. Agent searches for `per_tx_limit_exceeded` in docs. Finds it at line 56. Good.
2. Cause is clear: amount exceeds policy limit. Solution is clear: reduce amount or change policy.
3. Code example shows error detection with `instanceof` and `blockReason` check. Directly copyable.
4. Resolution requires human action (owner adjusts policy). The docs say this clearly.

**Verdict:** An agent can self-diagnose and determine next steps for every error on this page. The cause-solution mapping is clean and scannable. The horizontal rules between sections aid visual parsing. The page serves as a quick-reference lookup table, which is exactly what a developer needs when an error appears.

**Gap:** No mention of how to detect which error you have when not using the SDK (raw HTTP responses). The `blockReason` field is referenced in code but the JSON response shape is never shown. An agent using curl or Python would need to know the response structure.

---

## Score

**8/10**

Solid reference page. Well-structured cause-solution pairs with code examples. Deductions: retry logic is comment-only (-0.5), no raw HTTP response shape shown (-0.5), network error section could note non-Node environments (-0.5), Next Steps at minimum count (-0.5).
