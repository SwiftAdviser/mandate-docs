# QA Report: Error Codes

**File:** `/reference/error-codes.mdx`
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
| 6 | 3-5 cross-links | PARTIAL (2 cards) |
| 7 | Correct terminology | YES |
| 8 | Tables complete and scannable | YES |

## Findings

- **Line 118: Only 2 Next Steps cards.** Links to /sdk/errors and /reference/block-reasons. Needs at least one more. Candidates: /reference/rate-limits (for 429 handling), /guides/handle-errors, or /troubleshooting/common-errors.

Everything else is clean:

- Line 4: Description covers "HTTP status codes, error response format, and SDK error class mapping."
- Lines 11-19: Both response formats (policy block, general error) shown upfront with JSON examples. Good for developers who need to parse responses.
- Lines 34-46: HTTP status code table. 11 status codes with 4 columns: Status, Meaning, SDK Error Class, When It Happens. Covers 200, 202, 400, 401, 403, 404, 409, 410, 422, 429, 500.
- Lines 48-69: SDK error class hierarchy in ASCII tree format. Shows inheritance and key properties per class. Visually clear.
- Lines 71-79: Mapping rules in bullet list format. 5 rules covering how API responses map to SDK classes.
- Lines 83-113: Full error handling code example with all 5 error classes in correct specificity order (most specific first). Shows realistic recovery patterns.

## Developer Experience Notes

Excellent. This page serves two audiences well:

1. **API consumers (raw HTTP):** The status code table at line 34 maps HTTP codes to meanings. A developer receiving a 409 can find "Conflict: Duplicate intent hash or attempt to transition an intent in a wrong state."

2. **SDK consumers:** The class hierarchy at line 48 and the code example at line 83 show how to handle errors idiomatically. The comment about checking "specific subclasses before the base class" (line 83) prevents a common mistake.

The mapping rules at line 71 are particularly useful: they explain the non-obvious case where 422 maps to either `PolicyBlockedError` or `RiskBlockedError` depending on the `blockReason` value.

The 2-card Next Steps is the only structural gap. Adding /reference/rate-limits would complete the error-handling triangle (error codes + block reasons + rate limits).

## Score

**8.5/10**
