# Test Report: Choosing an Integration

**File:** guides/choosing-integration.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Choosing an Integration" |
| Frontmatter: sidebarTitle | PASS | "Choosing Integration" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 6 cards (cols=3) |
| Cross-links (3-5) | PASS | count: 15+ (heavy cross-linking throughout, all integrations linked) |
| Correct terminology | WARN | See findings below |
| Code examples quality | N/A | Decision guide, no code examples expected |
| Steps are followable | PASS | Clear decision tree with numbered steps |
| Error handling shown | N/A | Not a code guide |
| Developer clarity | PASS | Decision tree format is effective |

## Findings

### Medium: Terminology - "preflight" used in description

- **Line(s):** 33
- **Rule:** Use "validate" not "preflight" (unless explaining the alias)
- **Found:** `Two-phase enforcement (preflight gate, then validate) runs without any changes to your agent code.`
- **Fix:** Reword to: "Two-phase enforcement (validate gate, then full policy check) runs without any changes to your agent code." Or if "preflight" is the actual name of phase 1 in the plugin, add a parenthetical clarification.

### Low: Next Steps has 6 cards with cols=3

- **Line(s):** 94
- **Rule:** Writing guide shows CardGroup cols={2} in examples
- **Found:** `<CardGroup cols={3}>` with 6 cards
- **Fix:** This is a minor deviation from the template. For a guide that covers 11 integration paths, 6 cards in 3 columns is reasonable. No action needed, but noting for consistency.

### Low: No "Prerequisites" or "Before you start" section

- **Line(s):** (missing)
- **Rule:** Guides should mention prerequisites
- **Found:** The guide assumes the reader knows what Claude Code, OpenClaw, GOAT, AgentKit, etc. are. A brief note about needing a Mandate account or runtime key is missing.
- **Fix:** Add a one-line note: "You need a Mandate runtime key for all integration methods. See [Register Agent](/guides/register-agent) to get started."

## Developer Experience Notes

This is an excellent decision guide. The numbered steps ("stop at the first match") pattern is effective and saves time. The comparison table gives a quick overview of all 11 methods. The hook-based vs SDK-based architecture explanation is valuable for understanding the tradeoffs. As a developer, I can identify my integration path in under a minute. The Warning about SDK-based integrations needing explicit validate() calls is important and well-placed. The guide serves its purpose well as a routing page.

## Score
- Critical: 0, High: 0, Medium: 1, Low: 2
- **Overall:** WARN
