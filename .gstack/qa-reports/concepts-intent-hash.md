# Test Report: Intent Hash

**File:** concepts/intent-hash.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Intent Hash" |
| Frontmatter: sidebarTitle | PASS | "Intent Hash" |
| Frontmatter: description | PASS | Specific, includes keccak256 and attack vector |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | WARN | Line 9: 5 sentences in opening paragraph |
| Next Steps CardGroup | PASS | 4 cards at bottom |
| Cross-links (3-5) | PASS | count: 4 (all in CardGroup) |
| Correct terminology | PASS | All terms correct |
| Opens with "What is X?" | FAIL | "What is the intent hash?" - 71 words, exceeds 60-word limit |
| Code examples quality | PASS | Import shown, realistic values, function name matches SDK |
| Developer clarity | PASS | Canonical string format + mismatch table are excellent |

## Findings

### High: Opening paragraph exceeds 60-word limit
- **Line(s):** 9
- **Rule:** Open concept pages with "What is X?" answered in first 60 words
- **Found:** 71 words. The paragraph covers the definition, the mechanism, the scope limitation, and the attack vector it prevents.
- **Fix:** Split into two paragraphs. First paragraph (under 60 words): define the intent hash and its purpose. Second paragraph: explain the envelope swap attack it prevents. Move "This mechanism is used only in raw validation flows. Action-based validation does not require an intent hash." to the definition paragraph and trim other words, or move the attack explanation to paragraph 2.

### Medium: Opening paragraph exceeds 4 sentences
- **Line(s):** 9
- **Rule:** Short paragraphs (2-4 sentences max)
- **Found:** 5 sentences in the opening paragraph
- **Fix:** Same fix as above: split after "blocked with `intent_hash_mismatch`."

### Low: No inline cross-links in body text
- **Line(s):** entire file
- **Rule:** 3-5 cross-links (inline links in text and card groups)
- **Found:** All 4 cross-links are in the CardGroup only
- **Fix:** Add inline links: link "raw validation" (line 9) to /concepts/glossary#raw-validation, link "EnvelopeVerifierService" (line 48) to /concepts/architecture, link "circuit breaker" (line 48) to /concepts/glossary#circuit-breaker

## Developer Experience Notes
Excellent technical page. The canonical string format section (lines 15-42) is exactly what a dev needs when debugging hash mismatches. The mismatch causes table (lines 78-86) is a practical troubleshooting aid. The code example (lines 54-70) shows the correct import and realistic parameter values. The Warning and Note callouts (lines 87-93) preempt common questions. A dev working with raw validation would find this page highly actionable.

## Score
- Critical: 0, High: 1, Medium: 1, Low: 1
- **Overall:** WARN
