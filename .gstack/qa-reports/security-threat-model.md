# Test Report: Threat Model

**File:** /Users/krutovoy/Projects/mandate-docs/security/threat-model.mdx
**Section:** security
**Date:** 2026-03-26
**Status:** WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Threat Model" |
| Frontmatter: sidebarTitle | PASS | "Threat Model" |
| Frontmatter: description | PASS | One sentence, action-oriented |
| No em dashes (U+2014) | PASS | None found |
| No filler words | PASS | None found |
| Active voice / present tense | PASS | Consistent throughout |
| Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit |
| "Next Steps" CardGroup at bottom | FAIL | CardGroup exists (line 73) but labeled implicitly, no "## Next Steps" heading |
| 3-5 cross-links | PASS | 3 cards at bottom: prompt-injection, circuit-breaker, non-custodial |
| Concept opens with "What is X?" | PASS | First paragraph (line 7) defines threat model in opening sentence |
| Code examples: imports | N/A | No code examples on this page |
| Code examples: realistic names | N/A | No code examples |
| Terminology: "runtime key" | PASS | Not mentioned (appropriate) |
| Terminology: "validate" | PASS | Uses "validation" correctly |
| Terminology: "policy engine" | PASS | "policy engine" used at line 48 |
| Terminology: "circuit breaker" | PASS | Used correctly at lines 44, 69 |
| Terminology: "dashboard" | PASS | Not mentioned |
| Terminology: "block reason" | PASS | Uses "blockReason" (line 121-area context) implicitly |
| Question-based headings | PASS | All H2s are questions |
| Self-contained answer blocks | PASS | Each section answers its heading independently |
| Specific numbers | PASS | "18+ patterns", "six categories", "keccak256" |

## Findings

### medium: Missing "## Next Steps" heading above CardGroup
- **Line(s):** 73
- **Rule:** Page Structure: "Next Steps" card group at the bottom
- **Found:** CardGroup starts directly at line 73 with no heading
- **Suggested fix:** Add `## Next Steps` heading on line 72, before the CardGroup

### medium: No code examples on security overview page
- **Line(s):** entire page
- **Rule:** Code Examples: show imports, realistic names
- **Found:** Page is entirely prose. No code demonstrating how a developer interacts with threat defenses.
- **Suggested fix:** Consider adding a minimal code example showing how `validate()` returns block reasons for different threat categories, or showing a policy configuration that enables all defense layers. This is a security overview so code is optional, but even a short response JSON example would ground the concepts.

### low: "kill switch" in glossary context not tested
- **Line(s):** N/A
- **Rule:** Terminology: "circuit breaker" not "kill switch"
- **Found:** "kill switch" not used. Good. But the page says "emergency stop" at line 8 context of circuit-breaker card, which is acceptable.
- **Suggested fix:** None needed.

## Developer Experience Notes

As a developer running an AI agent with a real-money wallet, this page is a strong starting point. The threat table (lines 13-21) gives immediate clarity on what Mandate covers. The "What Mandate does NOT protect against" section (lines 52-58) is valuable: it explicitly calls out private key theft, smart contract bugs, and MEV. This honesty builds trust.

Gaps from a practitioner perspective:

1. **No severity ranking.** The six threats are listed flat. A developer wants to know: which is most likely? Which causes the most damage? A risk matrix (likelihood x impact) would help prioritize hardening efforts.

2. **No "what to do first" guidance.** After reading this page, a developer knows the threats but not the priority order for implementation. A sentence like "Start with policy enforcement and circuit breakers, then add risk scanning and envelope verification" would help.

3. **The "defense in depth" section (lines 62-71) is excellent** but does not explain what happens if the outermost layer (reason scanner) is disabled. Can a developer run without it? What is the minimum viable security configuration?

4. **Private key management (line 56) gets one sentence.** For agents handling real money, this is arguably the most critical gap. A link to the credential-management page or a dedicated key management guide would be valuable.

## Score

- Critical: 0
- High: 0
- Medium: 2
- Low: 1
- **Overall:** WARN (0 critical, 0 high, has medium findings)
