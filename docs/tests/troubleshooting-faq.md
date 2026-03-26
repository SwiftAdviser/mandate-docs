# QA Report: troubleshooting/faq.mdx

**Reviewed:** 2026-03-26
**Reviewer:** Claude Opus 4.6 (doc QA agent)

---

## Checklist

| # | Rule | Pass? | Notes |
|---|------|-------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS | All three present. Description mentions "20 most common questions" but page has 21 questions. |
| 2 | No em dashes (U+2014) | PASS | None found. |
| 3 | No filler words | PASS | None found. |
| 4 | Short paragraphs (2-4 sentences) | PASS | All within limit. Some answers are 1 sentence, which is fine for FAQ format. |
| 5 | "Next Steps" CardGroup at bottom | PASS | Present, 3 cards. |
| 6 | 3-5 cross-links | PASS | 4 inline links: /guides/fail-safe (line 19), /reference/chain-reference (line 67), /dashboard/policy-builder (line 100). Plus 3 Next Steps cards: /quickstart (line 193), /troubleshooting/common-errors (line 196), /guides/choosing-integration (line 199). |
| 7 | Terminology | PASS | Uses "runtime key", "policy engine", "validate", "intent", "dashboard" consistently. |
| 8 | Troubleshooting: FAQ-specific: are answers self-contained, accurate, complete? | PASS | See findings for details. |

---

## Findings

### Line 4: Description says "20" but page has 21 questions
The description reads "Answers to the 20 most common questions" but the page contains questions numbered 1-21. Question 21 (line 177, "What format does the amount field use?") appears to have been added after the description was written. Update the description to "21" or remove the count.

### Lines 9-13: Solana support answer is strong
Answers both validation methods, notes case sensitivity for non-EVM. Correctly scopes raw validation as EVM-only. Self-contained and citable.

### Lines 15-18: Fail-safe answer is definitive
"Block the transaction. Never fall back to calling the wallet directly." This is the single most important sentence in all of Mandate docs. Good that it appears in the FAQ.

### Lines 20-23: No-private-key answer
Clear explanation of action-based validation without signing. Names 4 wallet providers (Bankr, Locus, Sponge). These may become stale. Consider linking to an integrations page instead of hardcoding names.

### Lines 25-32: Testing answer with CLI example
Shows both the login and validate commands. Practical. Mentions testnet is free.

### Lines 34-40: Validate vs raw validate
Clean comparison. Correctly marks raw validate as deprecated. Uses bold for emphasis.

### Lines 44-46: Shared runtime key answer
"No." followed by reasoning. Direct and unambiguous.

### Lines 57-59: ERC-721/ERC-1155 answer
Covers NFTs through raw validation. Mentions the limitation of USD pricing for NFTs. Suggests alternatives (allowlist, selector-based controls).

### Lines 63-67: Chain support answer
Lists exact chain IDs. Mentions test vs live key mapping. Links to chain reference.

### Lines 93-96: Reason field storage answer
Clear about permanent audit log storage and LLM zero-retention. Addresses privacy concern directly.

### Lines 98-100: Default policy answer
Lists exact defaults with dollar amounts. Actionable: links to Policy Builder.

### Lines 120-136: Batch transactions answer with code
Shows the loop pattern. Important caveat: "Mandate tracks intents one at a time." Code is clear and copyable.

### Lines 143-171: ethers.js integration
Full working code example wrapping ethers.js signer. This is one of the most useful FAQ entries because ethers.js is the most common EVM library.

### Lines 177-188: Amount format table (Q21)
The table on lines 181-186 is excellent. Disambiguates between USD strings and raw token units across four methods. This is a common source of confusion and the table resolves it definitively.

### Lines 190-202: Next Steps has 3 cards
At minimum threshold. Consider adding /guides/handle-errors or /sdk/overview.

### Missing: No question about rate limits
Common FAQ topic for any API. If rate limits exist, they should be documented here.

### Missing: No question about webhook/event subscriptions
Developers often want to know if they can subscribe to events (approval decisions, circuit breaker trips) via webhooks rather than polling.

### Missing: No question about multi-sig or team-based ownership
Enterprise developers will ask about shared ownership of agents.

---

## Developer Experience Notes

**Scenario: Developer evaluating Mandate for the first time scans the FAQ.**

1. Questions are grouped by category (General, Keys, Chains, Approvals, Policies, Monitoring, Advanced). Good information architecture.
2. Numbered questions make it easy to reference: "see FAQ #5."
3. Most answers are self-contained: a developer does not need to click through to understand the answer.
4. Code examples appear where needed (Q4, Q7, Q12, Q17, Q19). They are not filler: each solves a real problem.
5. The amount format table (Q21) is a standout: this specific confusion comes up constantly in crypto dev and the table nails it.

**Scenario: AI agent needs to know if Mandate supports Solana.**

1. Agent searches FAQ for "Solana". Finds Q1 immediately.
2. Answer is complete: action-based yes, raw no, case-sensitivity note included.
3. No further page navigation needed.

**Verdict:** The FAQ is comprehensive and well-organized. It covers the questions a developer would actually ask during evaluation and early integration. The amount format table alone justifies the page. Main gap is the description/count mismatch and a few missing enterprise topics.

---

## Score

**8.5/10**

Strong FAQ with self-contained answers, good categorization, and useful code examples. The amount format table is exceptional. Deductions: description says 20 but has 21 questions (-0.5), no rate limit question (-0.5), Next Steps at minimum (-0.5).
