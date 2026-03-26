# QA Report: Intent States

**File:** `/reference/intent-states.mdx`
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

- Line 4: Description includes "9 states" as a specific number. Good GEO compliance.
- Line 9: Opening answers "What is the intent state machine?" with clear entry points for each validation type.
- Lines 13-27: Mermaid state diagram. Covers all transitions visually. Excellent for quick comprehension.
- Lines 31-41: State reference table with 5 columns: State, Description, TTL, Terminal, Entry Point. All 9 states documented. TTLs are explicit (24h, 15m, 1h, 10m, N/A, None).
- Lines 43-58: Transitions table with 4 columns: From, To, Trigger, Actor. 12 transitions. Matches the Mermaid diagram exactly.
- Lines 60-68: Terminal vs non-terminal states section. Clear list format.
- Lines 70-78: Quota behavior by terminal state. Covers what happens to reserved funds in each case. Critical information for financial correctness.
- Lines 80-92: Polling code example with realistic SDK methods.
- Lines 94-106: Next Steps with 3 cards.

## Developer Experience Notes

Excellent. This page is the gold standard for a state machine reference. Three views of the same information: visual (Mermaid), tabular (state reference), and transitions (from/to table). A developer debugging a stuck intent can check the TTL column, see the Mermaid diagram for valid transitions, and find the polling code example at the bottom.

The quota behavior table at line 72 answers a critical financial question: "What happens to my reserved budget if the intent fails?" This is the kind of detail that prevents support tickets.

One observation: the `allowed` state is marked as terminal (line 33, line 64), which differs from `reserved`. This is because action-based validation is fire-and-forget (no intent tracking), while raw validation tracks the full lifecycle. The page explains this, but a brief callout box highlighting this distinction could help developers who are migrating from raw to action-based validation.

## Score

**9.5/10**
