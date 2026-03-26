# Test Report: Snippet validate-response

**File:** snippets/validate-response.mdx
**Date:** 2026-03-26
**Status:** WARN
**Imported by:** guides/validate-transactions.mdx

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Correct terminology | PASS | Uses "intent" (not transaction request), "block reason" (not rejection reason), "validate()" (not preflight in the main text) |
| Code examples quality | PASS | Shows full `PreflightResult` interface with inline comments. Realistic field types. |
| Self-contained | PASS | H3 heading, interface definition, outcome table, and Note callout with cross-link. Complete reference block. |
| Consistent with importers | WARN | See findings below |

## Findings

### 1. PreflightResult type inconsistency with sdk/mandate-client.mdx

The snippet defines `PreflightResult` as:
```typescript
approvalReason?: string;
blockDetail?: string;
```

The sdk/mandate-client.mdx page defines the same interface as:
```typescript
approvalReason?: string | null;
blockDetail?: string | null;
```

The snippet uses optional-only (`?:`) while the SDK reference uses optional + nullable (`?: string | null`). These are semantically different in TypeScript. The SDK reference is likely the canonical source, so the snippet should match it.

### 2. Low import count

Only guides/validate-transactions.mdx imports this snippet. The `PreflightResult` interface is also defined inline in sdk/mandate-client.mdx (not using the snippet). This creates two sources of truth for the same type definition. Consider importing this snippet in sdk/mandate-client.mdx to ensure both pages show the same interface, or keep the snippet as the single source and import it everywhere the type is documented.

### 3. Note callout is well-placed

The `<Note>` at the end clarifies that `ApprovalRequiredError` is thrown automatically when `requiresApproval` is `true`, with a cross-link to `/guides/handle-approvals`. This aligns with the content in guides/validate-transactions.mdx where the snippet is placed between the "Approval required" section and the "How does validate() differ" section.

## Score

6/7 checks passed, 1 WARN. The type definition inconsistency with sdk/mandate-client.mdx should be resolved to avoid confusing developers who read both pages.
