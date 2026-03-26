# Test Report: Glossary

**File:** concepts/glossary.mdx
**Date:** 2026-03-26
**Status:** FAIL

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Glossary" |
| Frontmatter: sidebarTitle | PASS | "Glossary" |
| Frontmatter: description | PASS | Descriptive, lists key categories |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All definitions are 1-3 sentences |
| Next Steps CardGroup | FAIL | No Next Steps section at all |
| Cross-links (3-5) | PASS | count: 4 inline + 6 anchor = 10 total links |
| Correct terminology | WARN | "transaction request" on line 71, "preflight" on line 79 |
| Opens with "What is X?" | N/A | Glossary format, opens with alphabetical definitions |
| Code examples quality | N/A | No code examples |
| Developer clarity | WARN | Missing several important terms |

## Findings

### Critical: Missing Next Steps CardGroup
- **Line(s):** end of file (after line 154)
- **Rule:** Every page must have a "Next Steps" card group at the bottom
- **Found:** File ends at line 154 with the "Validate" definition. No `## Next Steps` section or `<CardGroup>`.
- **Fix:** Add a Next Steps section with cards linking to /concepts/architecture, /concepts/policy-engine, /quickstart, and /sdk/overview.

### High: Uses banned terminology "transaction request"
- **Line(s):** 71
- **Rule:** Use "intent" not "transaction request"
- **Found:** `A validated transaction request tracked through its lifecycle.`
- **Fix:** Rewrite to: "A validated action tracked through its lifecycle." or "A record of a validated transaction tracked through its lifecycle."

### Medium: "preflight" listed as intent state value without deprecation note
- **Line(s):** 79
- **Rule:** Use "validate" not "preflight" (unless explaining the alias)
- **Found:** `Possible values: reserved, approval_pending, approved, broadcasted, confirmed, failed, expired, rejected, preflight, allowed.`
- **Fix:** Add a parenthetical: `preflight (deprecated)` in the values list, consistent with the Preflight entry on line 111-113 which correctly marks it as deprecated.

### Medium: "Preflight" entry on line 111 is acceptable but could be clearer
- **Line(s):** 111-113
- **Rule:** Deprecated content handling
- **Found:** `**Preflight** Deprecated alias for validate(). Previously referred to the action-based validation endpoint for custodial wallets. Use validate() in all new integrations.`
- **Fix:** Acceptable as-is since it explains the deprecation. Consider wrapping in an `<Info>` callout per the writing guide's deprecated content rules.

### Low: Missing glossary entries for key concepts
- **Line(s):** entire file
- **Rule:** Developer clarity
- **Found:** Missing entries for: "Envelope swap" (attack described in intent-hash page), "Guard rules" (LLM judge feature), "Aegis" (risk screening), "EIP-8004" (reputation standard), "x402" (payment protocol). These terms appear in other concept pages but have no glossary definition.
- **Fix:** Add definitions for at least "Envelope swap", "Aegis", and "Guard rules" as these are referenced in multiple concept pages.

### Low: "emergency stop" used as primary definition for circuit breaker
- **Line(s):** 31
- **Rule:** "emergency stop" is acceptable in explanations per terminology guide
- **Found:** `An emergency stop mechanism.` as the opening definition
- **Fix:** Acceptable per guide rules (emergency stop allowed in explanations). No change required.

## Developer Experience Notes
The glossary is useful as a quick reference but has structural issues. A dev would find the alphabetical organization helpful for looking up specific terms. However, the missing Next Steps section breaks the navigation pattern that every other concept page follows. A dev reading through the concepts section sequentially would hit a dead end here. The missing entries for "Envelope swap", "Aegis", and "Guard rules" mean a dev encountering these terms in other pages has no glossary fallback.

## Score
- Critical: 1, High: 1, Medium: 2, Low: 2
- **Overall:** FAIL
