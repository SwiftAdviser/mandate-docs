# Test Report: Envelope Verification

**File:** /Users/krutovoy/Projects/mandate-docs/security/envelope-verification.mdx
**Section:** security
**Date:** 2026-03-26
**Status:** WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Envelope Verification" |
| Frontmatter: sidebarTitle | PASS | "Envelope Verification" |
| Frontmatter: description | PASS | One sentence, action-oriented |
| No em dashes (U+2014) | PASS | None found |
| No filler words | PASS | None found |
| Active voice / present tense | PASS | Consistent throughout |
| Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit |
| "Next Steps" CardGroup at bottom | FAIL | CardGroup at line 60, no "## Next Steps" heading |
| 3-5 cross-links | PASS | 3 cards: circuit-breaker, intent-hash, mandate-client |
| Concept opens with "What is X?" | PASS | Line 7 defines envelope verification in first sentence |
| Code examples: imports | FAIL | No code examples at all. Steps reference `rawValidate()` and `postEvent()` but show no code. |
| Code examples: realistic names | N/A | No code examples to evaluate |
| Terminology: "runtime key" | PASS | Not mentioned |
| Terminology: "validate" | PASS | Uses "rawValidate()" correctly |
| Terminology: "intent" | PASS | "intent" used correctly throughout (lines 19, 23, 40) |
| Terminology: "policy engine" | PASS | Used at line 58 |
| Terminology: "circuit breaker" | PASS | Used correctly (lines 13, 42) |
| Terminology: "dashboard" | PASS | Not mentioned |
| Question-based headings | PASS | All H2s are questions |
| Self-contained answer blocks | PASS | Each section stands alone |
| Specific numbers | PASS | "five steps", "10%", "four fields" |

## Findings

### high: No code examples for a developer-facing verification flow
- **Line(s):** 17-35
- **Rule:** Code Examples: show imports, realistic names
- **Found:** The page describes a 5-step flow (rawValidate, sign, postEvent, fetch, compare) but shows zero code. This is the most implementation-heavy security page and a developer cannot implement envelope verification from this documentation alone.
- **Suggested fix:** Add a complete CodeGroup showing the rawValidate + postEvent flow:
```typescript
import { MandateClient } from '@mandate.md/sdk';
import { Wallet } from 'ethers';

const mandate = new MandateClient({ runtimeKey: process.env.MANDATE_RUNTIME_KEY });
const wallet = new Wallet(process.env.AGENT_PRIVATE_KEY, provider);

// Step 1: Validate
const validation = await mandate.rawValidate({
  to: '0xRecipientAddress',
  value: '5000000',
  chainId: 84532,
  data: '0x...',
  reason: 'Monthly vendor payment for hosting',
});

// Step 2-3: Sign, broadcast, report
const tx = await wallet.sendTransaction(validation.txParams);
await mandate.postEvent(validation.intentId, tx.hash);
```

### medium: Missing "## Next Steps" heading above CardGroup
- **Line(s):** 60
- **Rule:** Page Structure: "Next Steps" card group at the bottom
- **Found:** CardGroup at line 60 with no heading
- **Suggested fix:** Add `## Next Steps` heading on line 59

### low: "raw validation flow" terminology could confuse newcomers
- **Line(s):** 10, 56
- **Rule:** Terminology consistency
- **Found:** "raw validation flow" is used but never formally defined on this page. It is contrasted with "action-based validation flow" (line 57) but a developer new to Mandate may not know which flow they are using.
- **Suggested fix:** Add a brief note at line 10: "The raw validation flow is used by agents that sign transactions locally (self-custodial). See [Choosing an Integration](/guides/choosing-integration) to determine which flow applies to your setup."

## Developer Experience Notes

As a developer with a wallet handling real money, envelope verification is one of the most important security features. This page explains the concept well but falls short on implementation guidance.

Critical gaps:

1. **No code at all.** This is the single biggest gap in the security section. The 5-step flow (lines 17-35) is described in prose but a developer needs to see the actual SDK calls. Without code, a developer must reverse-engineer the API from the SDK reference page. For a security-critical flow, this is unacceptable: incorrect implementation could silently disable verification.

2. **No error handling for the postEvent call.** What happens if `postEvent()` fails? Is the intent stuck in `reserved` state forever? Does it time out? A developer needs to know the failure modes and recovery path.

3. **Gas limit tolerance (line 34) is mentioned as "10%" but not explained.** Why 10%? Is this configurable? If a developer's gas estimation differs by 11%, the circuit breaker trips. This has real operational impact and needs more detail.

4. **No guidance on timing.** How long after broadcast should the developer call `postEvent()`? Is there a deadline? What if the transaction takes minutes to confirm on a congested network?

5. **The "does not apply to action-based flow" caveat (lines 55-58) raises a question:** What protection exists against tx swapping in the action-based flow? If a developer uses `validate()` instead of `rawValidate()`, is there no envelope verification? This gap should be explicitly addressed.

6. **No monitoring guidance.** How does a developer monitor for envelope mismatches in production? Are there dashboard alerts? Webhook events? Log entries to grep for?

## Score

- Critical: 0
- High: 1
- Medium: 1
- Low: 1
- **Overall:** FAIL (has high finding: missing code examples for implementation-critical security flow)
