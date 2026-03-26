# Test Report: Fail-Safe Rules

**File:** guides/fail-safe.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Fail-Safe Rules" |
| Frontmatter: sidebarTitle | PASS | "Fail-Safe Rules" |
| Frontmatter: description | PASS | Action-oriented, includes "fail-closed" keyword |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 3 cards |
| Cross-links (3-5) | WARN | count: 3 (inline: /integrations/claude-code, /integrations/openclaw, /sdk/errors; cards: /guides/handle-errors, /security/threat-model, /concepts/non-custodial) |
| Correct terminology | PASS | Uses correct terminology |
| Code examples quality | WARN | See findings below |
| Steps are followable | PASS | Clear rules, code pattern provided |
| Error handling shown | PASS | Both MandateError and network error branches shown |
| Developer clarity | PASS | Critical rules clearly stated |

## Findings

### Medium: Cross-links at minimum threshold

- **Line(s):** 69-81
- **Rule:** 3-5 cross-links to related pages
- **Found:** Only 3 cards in Next Steps. Inline links include /sdk/errors (in code comment, not a real link), /integrations/claude-code, /integrations/openclaw. Total unique cross-links: ~5, borderline.
- **Fix:** Add a 4th card linking to /guides/validate-transactions or /guides/ci-cd to strengthen the cross-link count.

### Medium: Code example uses spread syntax hiding the actual payload

- **Line(s):** 27
- **Rule:** Use realistic variable names, show complete examples
- **Found:** `const result = await client.validate({ ... });`
- **Fix:** Replace the spread with a concrete payload (action, amount, to, token, reason) so developers can copy-paste. The guide is about the error handling pattern around validate(), so the payload matters less, but a real payload improves readability.

### Low: The five rules are imported from a snippet and not visible in the page source

- **Line(s):** 13
- **Rule:** Self-contained answer blocks
- **Found:** `<FailSafe />` imports the actual rules. The page text says "must enforce five rules" but the rules themselves are in a snippet.
- **Fix:** This is not necessarily wrong (snippets are reusable), but for LLM/GEO optimization, the five rules should ideally be visible as text in this page too. Consider whether the snippet renders the rules inline. If so, this is fine.

## Developer Experience Notes

The page makes the most critical rule crystal clear: if the API is unreachable, block the transaction. The banking analogy (card terminal declining when network is down) is effective. The code pattern is practical and shows the correct branching for MandateError vs network errors. The plugin section explains how Claude Code and OpenClaw handle this automatically. As a developer, the testing tip (point SDK at invalid URL) is immediately actionable. The only gap is that the page leans heavily on the FailSafe snippet, so the core content depends on that snippet rendering correctly.

## Score
- Critical: 0, High: 0, Medium: 2, Low: 1
- **Overall:** WARN
