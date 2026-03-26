# QA Report: troubleshooting/intent-hash-mismatch.mdx

**Reviewed:** 2026-03-26
**Reviewer:** Claude Opus 4.6 (doc QA agent)

---

## Checklist

| # | Rule | Pass? | Notes |
|---|------|-------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS | All three present. Description mentions "7-point checklist." |
| 2 | No em dashes (U+2014) | PASS | None found. |
| 3 | No filler words | PASS | None found. |
| 4 | Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit. Longest is 2 sentences. |
| 5 | "Next Steps" CardGroup at bottom | PASS | Present, 3 cards. |
| 6 | 3-5 cross-links | PASS | 3 links: /concepts/intent-hash (line 142), /sdk/intent-hash (line 145), /troubleshooting/common-errors (line 148). |
| 7 | Terminology | PASS | Uses "intent hash", "raw validation", "runtime key" correctly throughout. |
| 8 | Troubleshooting: exact errors, step-by-step, cause-solution mapping | PASS | 7-step numbered checklist with code for each. |

---

## Findings

### Line 9: Strong opening paragraph
The first paragraph explains the error clearly in ~60 words. It names the endpoint, describes what the server does, and states the root cause class. This is excellent for GEO/LLM citation.

### Lines 11-13: Info callout is well-placed
Immediately tells developers using action-based validation to skip the page. Saves time.

### Lines 19-21: Canonical hash format shown
The exact format string is displayed, which is the single most important piece of information for debugging. Good.

### Lines 29-104: Checklist items are well-ordered
Items 1-3 are flagged as the most common causes (line 27). Each item has a "Wrong" and "Correct" code comparison. This pattern is highly scannable.

### Line 49: "Gas estimation may differ" heading is vague
The heading "Gas estimation may differ" reads as an observation, not an action item. Consider "Lock gas values before computing the hash" for consistency with the action-oriented debugging format.

### Line 108: "Mismatches should not occur"
Line 127: "mismatches should not occur unless the nonce is stale." This is a strong claim. If a developer uses the SDK function and still gets the error, this sentence may cause confusion. Consider "mismatches are unlikely unless the nonce is stale."

### Lines 129-137: Fallback debugging is excellent
The "Still getting mismatches?" section provides the canonical string construction for manual comparison. This is the right escape hatch when all 7 checks pass.

### Lines 139-151: Next Steps has exactly 3 cards
At the minimum threshold. A card linking to /guides/validate-transactions (showing full raw validation flow) would add value.

### Line 134: Long code line
The canonical string template literal on line 134 is very long. It may cause horizontal scrolling in rendered docs. Consider breaking it across multiple lines with concatenation.

---

## Developer Experience Notes

**Scenario: AI agent gets `intent_hash_mismatch` error on raw validation.**

1. Agent searches for "intent_hash_mismatch". Finds this dedicated page.
2. Info callout immediately tells agents using action-based validation this does not apply.
3. The canonical hash format on line 20 gives the exact string the server computes. Agent can compare.
4. The 7-point checklist is ordered by frequency. Agent works through items 1-3, which covers ~90% of cases.
5. Each checklist item shows wrong vs. correct code. Agent can diff against their implementation.
6. If all checks pass, the "Still getting mismatches?" section gives a logging approach for character-by-character comparison.
7. If the agent does not want to deal with any of this, the SDK function on line 111 is the recommended escape.

**Verdict:** This is the best-structured troubleshooting page in the set. The progressive debugging approach (common causes first, canonical format, SDK escape hatch, manual fallback) mirrors how a developer actually debugs. Every step has code. The page is self-contained: a developer should not need to leave it to fix their issue.

---

## Score

**9/10**

Excellent troubleshooting page. Clear progressive debugging flow, code for every step, strong opening for LLM citation. Deductions: one vague heading (-0.5), Next Steps at minimum count (-0.5).
