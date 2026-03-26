# Test Report: System Architecture

**File:** concepts/architecture.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "System Architecture" |
| Frontmatter: sidebarTitle | PASS | "Architecture" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | WARN | Line 15: 5 sentences in one paragraph |
| Next Steps CardGroup | PASS | 4 cards at bottom |
| Cross-links (3-5) | PASS | count: 4 (all in CardGroup) |
| Correct terminology | PASS | "emergency stop" on line 42 is acceptable in explanation context per guide |
| Opens with "What is X?" | PASS | "What is Mandate's architecture?" - 53 words, under 60 |
| Code examples quality | N/A | Mermaid diagram only, no TypeScript/Python code |
| Developer clarity | PASS | Clear overview of system flow, services table, auth layers |

## Findings

### Medium: Paragraph exceeds 4 sentences
- **Line(s):** 15
- **Rule:** Short paragraphs (2-4 sentences max)
- **Found:** "The core flow has three phases: validate, sign, confirm. The agent sends transaction details to the Mandate API. The policy engine runs 14 sequential checks. If all checks pass, the agent signs the transaction locally and broadcasts it to the blockchain. After broadcast, the agent reports the transaction hash back to Mandate for envelope verification."
- **Fix:** Split into two paragraphs after "sequential checks."

### Low: No inline cross-links in body text
- **Line(s):** entire file
- **Rule:** 3-5 cross-links to related pages (inline links in text and card groups)
- **Found:** All 4 cross-links are in the CardGroup only
- **Fix:** Add 1-2 inline links in body text (e.g., link "policy engine" to /concepts/policy-engine, link "intent" to /concepts/intent-lifecycle)

## Developer Experience Notes
Strong page for a dev building an AI agent. The services table (lines 37-49) gives a clear picture of what the backend does. The auth table (lines 56-60) answers the immediate question "how do I authenticate?" The mermaid diagram helps visualize the flow. A dev would understand the overall architecture after reading this page.

## Score
- Critical: 0, High: 0, Medium: 1, Low: 1
- **Overall:** WARN
