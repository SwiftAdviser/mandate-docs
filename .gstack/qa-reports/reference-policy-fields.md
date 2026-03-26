# QA Report: Policy Fields

**File:** `/reference/policy-fields.mdx`
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
| 6 | 3-5 cross-links | YES (3 cards + inline links) |
| 7 | Correct terminology | YES |
| 8 | Tables complete and scannable | YES |

## Findings

No violations found.

- Line 4: Description is action-oriented and includes "every configurable field." Good.
- Line 9: Opening paragraph answers "What is a policy?" in under 60 words. Includes default values.
- Lines 17-21: Spend limits table. 3 fields, each with Type, Default, Description. blockReason cross-references are inline (e.g., "blocked with `per_tx_limit_exceeded`").
- Lines 28-30: Address controls table. 2 fields.
- Lines 39-41: Action controls table. 2 fields. Both reference their blockReason values.
- Lines 46-49: Approval rules table. 3 fields.
- Lines 54-56: EVM transaction limits table. 2 fields. Clearly marked "raw validation only."
- Lines 61-62: Schedule field with JSON format example.
- Lines 69-70: Guard rules field with link to /guides/write-mandate-md.
- Lines 77-80: System fields table. 3 fields.
- Lines 86-105: Full example policy JSON with a plain-English explanation at line 107. This is exactly what a developer copying config needs.
- Lines 109-121: Next Steps with 3 cards.

Total: 16 policy fields documented across 7 category tables. Every field has Type, Default, and Description.

## Developer Experience Notes

Strong. The category grouping (Spend Limits, Address Controls, Action Controls, Approval Rules, EVM Limits, Schedule, Guard Rules, System Fields) mirrors the mental model a developer uses when configuring a policy. The full JSON example at line 86 ties everything together.

Cross-referencing is well done: each field's Description column mentions which blockReason it triggers, linking back to /reference/block-reasons conceptually. A developer configuring `spend_limit_per_tx_usd` immediately sees that exceeding it produces `per_tx_limit_exceeded`.

The Tip callout at line 32 about `allowed_addresses` being "the strongest protection against prompt injection" is valuable opinionated guidance. This is exactly the kind of recommendation the writing guide calls for.

One suggestion: consider adding a "required vs optional" column or indicator. Currently, developers must infer from defaults (null = optional, non-null = has a default). An explicit "Required" column would reduce ambiguity for first-time integrators.

## Score

**9/10**
