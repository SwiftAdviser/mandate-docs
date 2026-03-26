# Test Report: How Mandate Works

**File:** how-it-works.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "How Mandate Works" |
| Frontmatter: sidebarTitle | PASS | "How It Works" |
| Frontmatter: description | PASS | Detailed, action-oriented, keyword-rich |
| No em dashes | PASS | No U+2014 characters found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs 2-4 sentences |
| Next Steps CardGroup | PASS | CardGroup with 4 cards at bottom |
| Cross-links (3-5) | PASS | count: 7 (/concepts/reason-field, /reference/block-reasons, /guides/handle-approvals, /security/circuit-breaker, /guides/fail-safe, /concepts/policy-engine, /dashboard/policy-builder) |
| Correct terminology | WARN | One "emergency stop" usage in policy check list |
| Code examples quality | PASS | JSON response examples are clear and realistic |
| Developer clarity | PASS | Question-based headings match developer search queries. Mermaid diagram is helpful. |

## Findings

### medium: "emergency stop" used instead of "circuit breaker" in policy check description

- **Line(s):** 129
- **Rule:** Correct terminology (writing guide: "circuit breaker" not "kill switch, emergency stop")
- **Found:** `1. **Circuit breaker**: is the agent's emergency stop active?`
- **Fix:** Replace with `1. **Circuit breaker**: is the agent's circuit breaker active?` The writing guide says "emergency stop" is "acceptable in explanations" but here it is the primary label for the check, where "circuit breaker" should be used consistently.

### low: Concept page opens with question-heading, which is good GEO practice

- **Line(s):** 7
- **Rule:** GEO/LLM Optimization (definition first)
- **Found:** `## How does Mandate validate transactions?`
- **Fix:** No fix needed. The page opens with "How does Mandate validate transactions?" and answers it in the first paragraph. This satisfies the "What is X?" rule adapted to a "how it works" page.

## Developer Experience Notes

Strong conceptual page. As a developer, the three validation outcomes section (lines 76-123) is the most useful part: it shows exact JSON responses for allowed, blocked, and approval-required. This is what I would need to implement error handling correctly. The 14-check list on lines 128-143 is precise and ordered, which is valuable for debugging when something gets blocked. The mermaid sequence diagram on lines 11-33 provides a visual overview of the flow. The session keys comparison table on lines 45-54 effectively communicates the value add. The Warning on lines 72-74 about fail-safe behavior is well-placed and links to the guide. One observation: the page does not include TypeScript/SDK code examples for handling the three outcomes. A developer reading this page might want to see how to implement the switch in code, but this is appropriately deferred to the guides.

## Score

- Critical: 0, High: 0, Medium: 1, Low: 1
- **Overall:** WARN
