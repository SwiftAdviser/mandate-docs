# Test Report: Agent Reputation (ERC-8004)

**File:** /Users/krutovoy/Projects/mandate-docs/security/reputation.mdx
**Section:** security
**Date:** 2026-03-26
**Status:** WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Agent Reputation (ERC-8004)" |
| Frontmatter: sidebarTitle | PASS | "Reputation" |
| Frontmatter: description | PASS | One sentence, action-oriented |
| No em dashes (U+2014) | PASS | None found |
| No filler words | PASS | "significantly" at line 35 is borderline but not on the banned list |
| Active voice / present tense | PASS | Consistent |
| Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit |
| "Next Steps" CardGroup at bottom | FAIL | CardGroup at line 43, no "## Next Steps" heading |
| 3-5 cross-links | PASS | 3 cards: threat-model, approval-triggers, architecture |
| Concept opens with "What is X?" | PASS | Line 7 defines ERC-8004 in first sentence |
| Code examples: imports | FAIL | No code examples at all |
| Code examples: realistic names | N/A | No code |
| Terminology: "runtime key" | PASS | Not mentioned |
| Terminology: "validate" | PASS | "validation" used correctly |
| Terminology: "policy engine" | PASS | Used at lines 7, 39 |
| Terminology: "dashboard" | PASS | Not mentioned |
| Terminology: "circuit breaker" | PASS | Not mentioned |
| Terminology: "block reason" | PASS | Uses "reputation_critical" correctly (line 27) |
| Question-based headings | PASS | All H2s are questions |
| Self-contained answer blocks | PASS | Each section stands alone |
| Specific numbers | PASS | "5 minutes" cache, "three tiers" |

## Findings

### medium: Missing "## Next Steps" heading above CardGroup
- **Line(s):** 43
- **Rule:** Page Structure: "Next Steps" card group at the bottom
- **Found:** CardGroup at line 43 with no heading
- **Suggested fix:** Add `## Next Steps` heading on line 42

### medium: No code examples
- **Line(s):** entire page
- **Rule:** Code Examples: show imports
- **Found:** No code showing how reputation affects the validate response or how to handle reputation-related blocks/approvals.
- **Suggested fix:** Add a code example showing a validate response with reputation data:
```typescript
import { MandateClient } from '@mandate.md/sdk';

const mandate = new MandateClient({ runtimeKey: process.env.MANDATE_RUNTIME_KEY });
const result = await mandate.validate({ action: 'transfer', reason: 'Vendor payment' });

if (result.blockReason === 'reputation_critical') {
  logger.error('Agent reputation too low, transaction blocked');
}

if (result.requiresApproval && result.approvalTrigger === 'low_reputation') {
  logger.info('Low reputation: waiting for owner approval');
}
```

### medium: Threshold values are not specified
- **Line(s):** 22-28
- **Rule:** Specific numbers (GEO/LLM optimization)
- **Found:** The threshold table says "Above threshold", "Below threshold", "Below critical threshold" but never provides default values. A developer cannot assess their agent's risk without knowing the actual numbers.
- **Suggested fix:** Add default threshold values: "Good: score above 70 (default), Low: score between 30-70, Critical: score below 30" or whatever the actual defaults are. If the values are not fixed, state the range and how to check the current thresholds.

### low: ERC-8004 registration process is underspecified
- **Line(s):** 32-35
- **Rule:** Actionable mitigations
- **Found:** "Register your agent's wallet address following the ERC-8004 specification" does not tell the developer how. No contract address, no function call, no link to the specification.
- **Suggested fix:** Add a link to the ERC-8004 spec and/or a code example showing the registration call. At minimum: "See the [ERC-8004 specification](link) for registration details" with a contract address for supported chains.

## Developer Experience Notes

As a developer with an agent handling real money, reputation scoring is a useful additional signal but this page leaves too many questions unanswered.

Key gaps:

1. **No default threshold values.** The table at lines 22-28 is the most important part of this page, and the actual numbers are missing. A developer reading this cannot determine whether their agent would pass or fail reputation checks. This is a significant gap for security planning.

2. **Registration is a black box.** The page says registration "reduces friction significantly" (line 35) but provides no registration guide, no contract address, no transaction to send. A developer cannot act on this advice.

3. **No discussion of reputation manipulation.** Can an attacker inflate their reputation score? Can they grief a legitimate agent's reputation? For an on-chain system, these attack vectors should be addressed.

4. **Cache invalidation gap.** The page says reputation is cached for 5 minutes (line 41). What happens if a developer's reputation drops to critical during a 5-minute window? Transactions could be approved with stale reputation data. The page should acknowledge this and explain why 5 minutes is an acceptable trade-off.

5. **"Emerging standard" framing (line 7) raises trust concerns.** If ERC-8004 is still emerging, what is the fallback behavior? Is Mandate dependent on this standard being finalized? A developer investing in reputation registration wants to know the standard is stable.

6. **No subgraph address or query example.** The ReputationService "queries The Graph" (line 10) but there is no subgraph URL, no example GraphQL query, no way for a developer to verify their own reputation independently.

## Score

- Critical: 0
- High: 0
- Medium: 3
- Low: 1
- **Overall:** WARN (0 critical, 0 high, has medium findings)
