# Test Report: The Reason Field

**File:** concepts/reason-field.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "The Reason Field" |
| Frontmatter: sidebarTitle | PASS | "Reason Field" |
| Frontmatter: description | PASS | Specific, includes key differentiator claim |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 4 sentences |
| Next Steps CardGroup | PASS | 4 cards at bottom |
| Cross-links (3-5) | PASS | count: 4 (all in CardGroup) |
| Correct terminology | PASS | "emergency stop" on line 82 is acceptable in explanation context |
| Opens with "What is X?" | WARN | "What is the reason field?" - 62 words, slightly over 60-word limit |
| Code examples quality | N/A | No code, comparison tables and examples only |
| Developer clarity | PASS | Excellent attack scenario walkthrough |

## Findings

### Medium: Opening paragraph exceeds 60-word limit
- **Line(s):** 9
- **Rule:** Open concept pages with "What is X?" answered in first 60 words
- **Found:** 62 words in the first paragraph
- **Fix:** Trim 2-3 words. The phrase "written by the agent at the moment it decides to make a transaction" can be shortened to "written by the agent at decision time."

### Low: No inline cross-links in body text
- **Line(s):** entire file
- **Rule:** 3-5 cross-links (inline links in text and card groups)
- **Found:** All 4 cross-links are in the CardGroup only
- **Fix:** Add inline links: link "policy engine" (line 10) to /concepts/policy-engine, link "session keys" (line 11) to the comparison table, link "circuit breaker" (line 82) to /concepts/glossary#circuit-breaker

### Low: Line 82 paragraph is 4 sentences but dense
- **Line(s):** 82
- **Rule:** Developer clarity
- **Found:** `The decline message is adversarial by design. It explicitly states that the instruction did not come from the legitimate operator and that the agent must halt immediately. Even if the agent's reasoning is compromised, the Mandate response pushes back against continued exploitation. For circuit_breaker_active, the decline message states that the owner has activated an emergency stop and no further transactions should be attempted.`
- **Fix:** Consider splitting the `circuit_breaker_active` detail into its own sentence or callout, as it covers a different block reason than the rest of the paragraph.

## Developer Experience Notes
One of the strongest concept pages. The session key comparison table (lines 20-28) immediately shows a dev why the reason field matters. The attack scenario (lines 15-29) is concrete and memorable. The "good reasons" vs "weak reasons" section (lines 58-69) gives actionable guidance. A dev building an AI agent would understand exactly what to put in the reason field and why it matters for security.

## Score
- Critical: 0, High: 0, Medium: 1, Low: 2
- **Overall:** WARN
