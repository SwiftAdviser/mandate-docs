# QA Report: dashboard/agents.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 0 inline = 3) |
| 7 | Correct terminology | PASS |
| 8 | UI elements clearly described, step-by-step actions | PASS |

## Findings

### PASS: All checks pass
No em dashes, no filler words, correct terminology throughout. Uses "runtime key" consistently.

### GOOD: Step-by-step for key regeneration (lines 46-51)
Clear numbered steps for a sensitive operation. The Warning callout on line 53-55 correctly flags the instant revocation risk.

### GOOD: Agent list display table (lines 29-38)
Enumerates card fields clearly. Helpful for users scanning the UI.

### MINOR: Line 65 has an awkward sentence
Line 65: "a test key rejected on mainnet, a live key rejected on testnet." This reads as a fragment. Missing verb: "is rejected" for both clauses.

### MINOR: No screenshot reference for agent card layout
The "Agent list display" section (line 28) describes fields but a screenshot would anchor the description visually. The table is good, but a visual reference would reduce ambiguity about layout.

### NOTE: Cross-links are exactly at the minimum (3)
All 3 links are in the Next Steps cards. No inline links in body text. Adding an inline link to the policy builder from the "What is an agent" section or linking to the glossary would strengthen discoverability.

## Developer Experience Notes

- Strong page overall. The create/claim/edit/regenerate/delete lifecycle is well-covered.
- The claim flow explanation (lines 21-25) is clear and addresses a non-obvious workflow (programmatic registration + human claiming).
- Test vs live keys section (lines 63-65) is important but thin. A developer would want to know: can I convert a test agent to live? Can one agent have both? The answer to these questions is missing.
- No mention of agent limits. How many agents can I create? Is there a plan-based cap?
- Missing: bulk operations. If I have 20 agents, can I regenerate keys in bulk? Delete in bulk?

## Score

**8.5/10** - Well-structured, compliant page covering the full agent lifecycle. Minor grammar fix needed on line 65. Adding inline cross-links and a test-vs-live conversion FAQ would make it excellent.
