# Test Report: Intent Lifecycle

**File:** concepts/intent-lifecycle.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Intent Lifecycle" |
| Frontmatter: sidebarTitle | PASS | "Intent Lifecycle" |
| Frontmatter: description | PASS | Descriptive, includes key terms |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 4 sentences |
| Next Steps CardGroup | PASS | 4 cards at bottom |
| Cross-links (3-5) | PASS | count: 4 (all in CardGroup) |
| Correct terminology | WARN | Line 9: "validated transaction request" uses banned term |
| Opens with "What is X?" | PASS | "What is an intent?" - 51 words, under 60 |
| Code examples quality | N/A | Mermaid state diagram only, no code |
| Developer clarity | PASS | State machine diagram + table is excellent |

## Findings

### High: Uses banned terminology "transaction request"
- **Line(s):** 9
- **Rule:** Use "intent" not "transaction request"
- **Found:** `An intent represents a validated transaction request tracked through its full lifecycle.`
- **Fix:** Rewrite to: "An intent is a validated action tracked through its full lifecycle." or "An intent represents a transaction that Mandate validates and tracks through its full lifecycle."

### Low: No inline cross-links in body text
- **Line(s):** entire file
- **Rule:** 3-5 cross-links (inline links in text and card groups)
- **Found:** All 4 cross-links are in the CardGroup only
- **Fix:** Add inline links to related concepts in body text (e.g., link "policy engine" on line 15, "quota" on line 72, "circuit breaker" on line 66)

### Low: "allowed" listed as terminal state in table but not in prose
- **Line(s):** 39, 49
- **Rule:** Developer clarity
- **Found:** Table shows `allowed` with TTL "24 hours" and Terminal "Yes", but the prose on line 49 lists it as terminal. The mermaid diagram (line 21) shows `allowed` as an endpoint with no transitions out. This is consistent but could confuse devs: a "terminal" state with a 24-hour TTL is unusual.
- **Fix:** Add a brief note explaining that `allowed` is terminal for the action-based flow because no further state transitions are tracked (the agent handles signing independently).

## Developer Experience Notes
Very strong page. The state diagram (lines 17-31) and states table (lines 37-47) give a dev everything needed to understand how intents progress. The quota interaction section (lines 69-74) is a practical detail that saves debugging time. The transition actor table (lines 55-64) clearly answers "who triggers what." A dev building an agent would understand the full lifecycle after reading this.

## Score
- Critical: 0, High: 1, Medium: 0, Low: 2
- **Overall:** WARN
