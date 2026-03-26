# QA Report: Approval Triggers

**File:** `/reference/approval-triggers.mdx`
**Date:** 2026-03-26
**Status:** PASS

## Checklist

| # | Rule | Pass |
|---|------|------|
| 1 | Frontmatter: title, sidebarTitle, description | YES |
| 2 | No em dashes (U+2014) | YES |
| 3 | No filler words | YES |
| 4 | Short paragraphs (2-4 sentences) | YES |
| 5 | "Next Steps" CardGroup at bottom | YES |
| 6 | 3-5 cross-links | YES (3 cards) |
| 7 | Correct terminology | YES |
| 8 | Tables complete and scannable | YES |

## Findings

No violations found.

- Line 4: Description includes "7 conditions" as a specific number. Good GEO compliance.
- Line 9: Opening paragraph clearly distinguishes soft blocks (approval triggers) from hard blocks in under 60 words.
- Lines 15-23: Main reference table covers all 7 triggers with 4 columns: Trigger, Condition, Policy Field, Who Configures. Every trigger has its policy field documented or marked as `_(automatic)_`.
- Lines 25-51: Each trigger gets its own H3 with a 2-3 sentence explanation and concrete examples (e.g., "set to 500 and a $750 transfer triggers approval"). Good developer clarity.
- Lines 53-63: "Multiple triggers" section with JSON example. Covers an important edge case.
- Lines 65-77: Next Steps with 3 cards to /guides/handle-approvals, /dashboard/approvals, /reference/policy-fields.

## Developer Experience Notes

Good. The table at line 15 is immediately scannable: a developer who sees `amount_above_threshold` in an API response can find the row, see which policy field controls it, and know who configures it. The individual H3 sections below add helpful context without bloating the table.

Suggestion: The page does not include a code example showing how to detect and handle an approval trigger response in the SDK. A short `ApprovalRequiredError` snippet (similar to the one in error-codes.mdx) would complete the developer workflow: see trigger in table, understand what it means, know how to handle it in code. The "Handle Approvals" card link partially covers this, but inline code would be more self-contained.

The relationship between approval triggers and block reasons is well-delineated at line 11: "Approval triggers only fire after all hard checks pass." This prevents confusion.

## Score

**8.5/10**
