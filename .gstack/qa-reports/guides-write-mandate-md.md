# Test Report: Writing MANDATE.md Policy Files

**File:** guides/write-mandate-md.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Writing MANDATE.md Policy Files" |
| Frontmatter: sidebarTitle | PASS | "MANDATE.md" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 4 cards |
| Cross-links (3-5) | PASS | count: 5 (inline: /dashboard/mandate-md-editor, /dashboard/policy-builder, /reference/block-reasons, /dashboard/insights; cards: 4) |
| Correct terminology | PASS | Uses correct terminology throughout |
| Code examples quality | PASS | Realistic examples with specific addresses and amounts |
| Steps are followable | WARN | See findings below |
| Error handling shown | N/A | Not a code integration guide |
| Developer clarity | WARN | See DX notes |

## Findings

### Medium: Block reason terminology inconsistency with other guides

- **Line(s):** 163
- **Rule:** Consistent terminology across guides
- **Found:** `Exceeding per-transaction limit returns spend_limit_exceeded`
- **Fix:** The handle-errors guide uses `per_tx_limit_exceeded` as the block reason code. This page uses `spend_limit_exceeded`. These should be consistent. Verify which is the actual API value and use it everywhere.

### Medium: Missing step - how to actually deploy/apply MANDATE.md

- **Line(s):** (missing)
- **Rule:** Steps are sequential and followable
- **Found:** The guide explains the syntax and examples thoroughly, but never explains *how* the MANDATE.md file gets picked up. Does the scanner read it? Does the CLI upload it? Does the dashboard sync it? Line 11 mentions "Place it in your project root or edit it in the dashboard editor" but the mechanism is unclear.
- **Fix:** Add a section "How to apply your MANDATE.md" that explains: (1) place file in project root, (2) the scanner detects it as a protection signal, (3) to push rules to the policy engine, use CLI `npx @mandate.md/cli push` or the dashboard editor.

### Low: No code examples for programmatic use

- **Line(s):** (missing)
- **Rule:** Code examples with imports shown
- **Found:** All code examples are Markdown syntax. No TypeScript/Python/CLI examples showing how to programmatically load or reference the MANDATE.md file.
- **Fix:** Add a CLI example: `npx @mandate.md/cli push --file MANDATE.md` or similar, to show how the file becomes an active policy.

## Developer Experience Notes

The guide is excellent as a reference for MANDATE.md syntax. The three use case examples (DeFi trader, payroll, shopping) are immediately useful and cover common patterns. The section mapping table is a strong reference. However, the critical gap is the deployment story. As a developer, after writing my MANDATE.md file, I do not know what to do with it. Does dropping it in the project root automatically enforce it? Do I need to push it somewhere? The guide needs a "what to do after writing" step to close the loop.

## Score
- Critical: 0, High: 0, Medium: 2, Low: 1
- **Overall:** WARN
