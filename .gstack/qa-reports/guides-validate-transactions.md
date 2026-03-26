# Test Report: Validate Transactions

**File:** guides/validate-transactions.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Validate Transactions" |
| Frontmatter: sidebarTitle | PASS | "Validate Transactions" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 4 cards |
| Cross-links (3-5) | PASS | count: 6+ (inline: /dashboard/policy-builder, /reference/block-reasons, /dashboard/approvals, /dashboard/audit-log, /sdk/mandate-client; cards: 4) |
| Correct terminology | WARN | See findings below |
| Code examples quality | PASS | Imports shown, realistic names, success + error paths |
| Steps are followable | PASS | Clear 3-outcome pattern |
| Error handling shown | PASS | Full error handling with all error types |
| Developer clarity | WARN | See DX notes |

## Findings

### Medium: Terminology - "PreflightPayload" uses banned term "preflight"

- **Line(s):** 24, 106
- **Rule:** Use "validate" not "preflight" (unless explaining the alias)
- **Found:** `Pass a PreflightPayload` (line 24), `What fields does PreflightPayload accept?` (line 106)
- **Fix:** This appears to be the actual SDK type name, so it may be unavoidable. However, line 24 should clarify this is an SDK type name. Line 106 heading could be reworded to "What fields does the validate payload accept?" with a note that the SDK type is named `PreflightPayload`.

### Low: Terminology - "preflight" used in comparison table

- **Line(s):** 173
- **Rule:** Use "validate" not "preflight" (unless explaining the alias)
- **Found:** `The validate() method (also called preflight) is the primary...`
- **Fix:** This is acceptable per the rule "(unless explaining the alias)" but worth noting. The table on line 175 header says "validate() (recommended)" which is correct.

### Low: CodeGroup tab order - CLI before Python

- **Line(s):** 26-104
- **Rule:** CodeGroup tab order: TypeScript SDK, Python, CLI, curl
- **Found:** Order is TypeScript, CLI, Python, curl
- **Fix:** Move Python tab before CLI tab.

### Low: Missing prerequisite mention

- **Line(s):** (missing)
- **Rule:** Guides should mention prerequisites
- **Found:** No mention that you need to have registered an agent and obtained a runtime key first.
- **Fix:** Add a brief note or link: "Before validating, register your agent and obtain a runtime key. See [Register Agent](/guides/register-agent)."

## Developer Experience Notes

This is the strongest guide in the set. The three-outcome pattern (allowed, blocked, approval required) is clearly explained with code for each. The comparison table between validate() and rawValidate() is valuable. Best practices section is practical and specific. As a developer, I can follow this end-to-end: get a client, call validate, handle each outcome. The only gap is that the guide assumes I already have a runtime key without explicitly linking to the registration step.

## Score
- Critical: 0, High: 0, Medium: 1, Low: 3
- **Overall:** WARN
