# Test Report: Snippet fail-safe

**File:** snippets/fail-safe.mdx
**Date:** 2026-03-26
**Status:** PASS
**Imported by:** guides/fail-safe.mdx, guides/handle-errors.mdx, guides/validate-transactions.mdx

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Correct terminology | PASS | Uses "validate()" (not preflight), "block reason" (not rejection reason), "circuit breaker" (not kill switch) |
| Code examples quality | N/A | No code examples, only a numbered rule list inside a Warning callout |
| Self-contained | PASS | Fully self-contained Warning block with 5 numbered rules. No external context needed. |
| Consistent with importers | PASS | All 3 importing pages use it to present the non-negotiable rules. Surrounding content in each page is consistent with the rules listed. |

## Findings

No issues found. This is a clean, self-contained snippet consisting of a single `<Warning>` callout with 5 numbered fail-safe rules. The content is purely declarative and works in any context.

Each importing page provides additional context around the snippet:
- guides/fail-safe.mdx: Uses it as the primary definition, then expands with "why fail-closed" and implementation patterns.
- guides/handle-errors.mdx: Places it in the "Fail-safe rules" section near the bottom, followed by a reinforcing paragraph.
- guides/validate-transactions.mdx: Places it at the top of the page, right after the introductory section, establishing the rules before showing any code.

All three placements are contextually appropriate. The snippet's neutral, rule-based tone works well in all positions.

Rule 5 mentions `postEvent()`, which is a method on `MandateClient`. This is consistent with the SDK reference pages. The term "envelope verification" is used, which also appears in sdk/mandate-client.mdx.

## Score

7/7 checks passed. No action needed.
