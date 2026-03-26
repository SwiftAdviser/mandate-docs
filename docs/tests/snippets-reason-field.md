# Test Report: Snippet reason-field

**File:** snippets/reason-field.mdx
**Date:** 2026-03-26
**Status:** PASS
**Imported by:** guides/validate-transactions.mdx

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Correct terminology | PASS | Uses "reason field" (not justification/rationale), "policy engine" (not rules engine), "dashboard" (not admin panel) |
| Code examples quality | PASS | Shows `client.validate()` with realistic reason string including invoice number and vendor name. Imports not shown, but the snippet complements the surrounding code on the importing page which already has full imports. |
| Self-contained | PASS | H3 heading, 3-purpose numbered list, code example, Warning callout, and cross-links. Complete explanation. |
| Consistent with importers | PASS | validate-transactions.mdx places this after the PreflightPayload table, which mentions the reason field. The snippet expands on that mention with full detail. |

## Findings

No issues found. The snippet is well-structured with:

1. An H3 heading ("The `reason` field") that fits as a subsection in its importing page.
2. A clear opening sentence establishing the field's significance ("max 1,000 characters", "core differentiator from session keys").
3. A numbered list of 3 purposes: audit trail, prompt injection detection, policy learning.
4. A minimal code example showing a realistic reason value.
5. A Warning callout about prompt injection blocking.
6. Cross-links to `/concepts/reason-field` and `/security/prompt-injection`.

The code example omits imports (no `import { MandateClient }...`), using `client.validate()` directly. This works because the snippet is imported into a page that already establishes the `client` variable in prior code blocks. However, if this snippet were imported into a page without that context, the `client` reference would be unexplained. Since only guides/validate-transactions.mdx imports it (where `client` is well-established), this is acceptable.

Only 1 page imports this snippet. Consider using it in sdk/mandate-client.mdx where the `reason` field is described, or in the quickstart page.

## Score

7/7 checks passed. No action needed.
