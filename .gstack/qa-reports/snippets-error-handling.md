# Test Report: Snippet error-handling

**File:** snippets/error-handling.mdx
**Date:** 2026-03-26
**Status:** PASS
**Imported by:** guides/handle-errors.mdx, guides/validate-transactions.mdx, sdk/mandate-client.mdx

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Correct terminology | PASS | Uses "runtime key" (not API key), "block reason" (not rejection reason), "dashboard" (not admin panel) |
| Code examples quality | PASS | All 5 error classes imported, realistic variable names, both success and error paths shown |
| Self-contained | PASS | Opens with explanatory sentence, includes full code block with imports, and ends with a reference table and cross-link |
| Consistent with importers | PASS | All 3 importing pages use the snippet in error-handling sections. The error classes and patterns match the surrounding content in each page. |

## Findings

No issues found. This is a well-structured snippet:

1. Opens with a one-line description: "The SDK throws typed errors you can catch with `instanceof`."
2. Shows a complete TypeScript example with all 5 error classes imported and handled.
3. Includes a summary table mapping error classes to HTTP status codes and trigger conditions.
4. Ends with a cross-link to `/sdk/errors` for full details.

The code example uses realistic values: `runtimeKey` from env, `action: 'transfer'`, `amount: '100'`, `reason: 'Payment for API access'`. Variable names are descriptive (`err`, `client`, `result`).

The error handling order in this snippet (PolicyBlockedError first) differs from the order in guides/handle-errors.mdx page body (CircuitBreakerError first). The page body explains that order matters and checks specific subclasses before base. The snippet uses a different order but is correct since all subclasses are checked before the base `MandateError`. This is not a conflict, as the snippet serves as a quick reference, while the page body provides the production-recommended ordering.

## Score

7/7 checks passed. No action needed.
