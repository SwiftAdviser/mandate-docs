# Test Report: Non-Custodial Model

**File:** concepts/non-custodial.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Non-Custodial Model" |
| Frontmatter: sidebarTitle | PASS | "Non-Custodial" |
| Frontmatter: description | PASS | Clear, action-oriented |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | FAIL | Lines 11 and 30 exceed 4 sentences |
| Next Steps CardGroup | PASS | 4 cards at bottom |
| Cross-links (3-5) | PASS | count: 4 (all in CardGroup) |
| Correct terminology | PASS | All terms correct |
| Opens with "What is X?" | PASS | "What does non-custodial mean?" - 49 words, under 60 |
| Code examples quality | N/A | No code examples |
| Developer clarity | PASS | Comparison table and threat analysis are strong |

## Findings

### High: Paragraph exceeds 4-sentence limit
- **Line(s):** 11-12
- **Rule:** Short paragraphs (2-4 sentences max)
- **Found:** `This is not a theoretical claim. The Mandate API has no endpoint that accepts a private key. The validate endpoint receives action metadata, a reason string, and optionally a destination address and amount. The validate/raw endpoint receives unsigned transaction parameters and an intent hash. Neither endpoint requires or accepts key material.`
- **Fix:** Split after "private key." Start new paragraph at "The `validate` endpoint receives..."

### High: Numbered list reads as a long paragraph
- **Line(s):** 30-35
- **Rule:** Short paragraphs (2-4 sentences max)
- **Found:** The numbered list items (steps 1-4) each contain 2 sentences, creating a dense block of 12 sentence-equivalents. While numbered lists are technically not paragraphs, this block is visually heavy.
- **Fix:** This is borderline. The numbered list format is appropriate here. Consider adding a blank line between list items for readability, or no change needed since numbered lists are structurally different from paragraphs.

### Low: No inline cross-links in body text
- **Line(s):** entire file
- **Rule:** 3-5 cross-links (inline links in text and card groups)
- **Found:** All 4 cross-links are in the CardGroup only
- **Fix:** Add inline links: link "14 policy checks" (line 30) to /concepts/policy-engine, link "envelope verification" (line 35) to /concepts/glossary#envelope-verification, link "circuit breaker" (line 35) to /concepts/glossary#circuit-breaker

## Developer Experience Notes
Good page for understanding the trust model. The comparison table (lines 15-22) is the most valuable element: a dev immediately sees how Mandate differs from custodial wallets and session keys. The validation flow steps (lines 30-35) are practical. The "why does this matter" section (lines 38-43) ties the model to the real threat landscape for AI agents. A dev would understand Mandate's security posture after reading this.

## Score
- Critical: 0, High: 2, Medium: 0, Low: 1
- **Overall:** WARN
