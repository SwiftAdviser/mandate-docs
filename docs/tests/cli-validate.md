# QA Report: cli/validate.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline link to /reference/block-reasons) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 4**: Description mentions "preflight" in parentheses: "Supports preflight (action-based) and raw EVM modes." The terminology guide says "validate" not "preflight (unless explaining the alias)". This usage is borderline acceptable since it is explaining the mode name, but in the frontmatter description it reads like the primary term.
- **Line 12**: Section heading "Preflight mode (default, recommended)" uses "preflight" prominently. The terminology guide allows it when "explaining the alias," and this heading is doing that. Acceptable but could be clearer by leading with "validate" terminology.
- **Line 9-10**: Opening paragraph covers all three outcomes (intentId, blockReason, approval). Excellent for developer orientation.
- **Line 26-33**: Options table is complete for preflight mode.
- **Line 35-69**: Three output examples (success, blocked, approval required) cover all paths. The `next` field in approval output (line 67) tells agents exactly what to do.
- **Line 73-79**: Reason field section is strong. Explains why it matters, not only that it is required. Warning callout reinforces.
- **Line 81-121**: Raw mode section is properly marked deprecated with `<Info>` callout. Thorough flag tables.
- **Line 55**: Inline link to block reasons reference. Good cross-link.

## Developer Experience Notes

- **Best CLI page in the set**: Covers preflight and raw modes, all three response types, flags for both modes, and the reason field. A developer can go from zero to validated transaction with this page alone.
- **The reason field section (lines 73-79)**: Excellent. Tells me the policy engine scans the reason text, gives a good/bad example, and warns about omission. This is the kind of actionable detail that saves debugging time.
- **Minor**: No explicit prerequisite section. A developer must infer they need `login` + `activate` first. Other pages (like `activate`) have a Note callout about auth. This page should too, or link to the overview's credential section.

## Score

**9/10**

Comprehensive reference. Minor terminology quibble with "preflight" in the description. Missing explicit prerequisites note.
