# Test Report: Circuit Breaker

**File:** /Users/krutovoy/Projects/mandate-docs/security/circuit-breaker.mdx
**Section:** security
**Date:** 2026-03-26
**Status:** WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Circuit Breaker" |
| Frontmatter: sidebarTitle | PASS | "Circuit Breaker" |
| Frontmatter: description | PASS | One sentence, action-oriented |
| No em dashes (U+2014) | PASS | None found |
| No filler words | PASS | None found |
| Active voice / present tense | PASS | Consistent |
| Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit |
| "Next Steps" CardGroup at bottom | FAIL | CardGroup at line 40, no "## Next Steps" heading |
| 3-5 cross-links | PASS | 3 cards: dashboard controls, envelope-verification, troubleshooting |
| Concept opens with "What is X?" | PASS | Line 7 defines circuit breaker in first sentence |
| Code examples: imports | FAIL | API endpoints shown (lines 33-36) but no SDK code with imports |
| Code examples: realistic names | PASS | API endpoint uses `{agentId}` placeholder, acceptable |
| Terminology: "runtime key" | PASS | Correctly distinguishes "runtime key auth" from "dashboard auth" (line 38) |
| Terminology: "validate" | PASS | "validate()" used correctly (line 7) |
| Terminology: "policy engine" | PASS | Used at line 27 |
| Terminology: "dashboard" | PASS | Used correctly throughout |
| Terminology: "circuit breaker" | PASS | Correct term used throughout |
| Terminology: "kill switch" | PASS | Not used |
| Question-based headings | PASS | All H2s are questions |
| Self-contained answer blocks | PASS | Each section stands alone |
| Specific numbers | PASS | "30-second TTL", "HTTP 403" |

## Findings

### medium: Missing "## Next Steps" heading above CardGroup
- **Line(s):** 40
- **Rule:** Page Structure: "Next Steps" card group at the bottom
- **Found:** CardGroup starts at line 40 with no heading
- **Suggested fix:** Add `## Next Steps` heading on line 39

### medium: No SDK code example for circuit breaker interaction
- **Line(s):** 33-36
- **Rule:** Code Examples: show imports, realistic names
- **Found:** Only raw API endpoints are shown. No TypeScript/Python example demonstrating how to check circuit breaker status or handle `CircuitBreakerError` in agent code.
- **Suggested fix:** Add a CodeGroup:
```typescript
import { MandateClient, CircuitBreakerError } from '@mandate.md/sdk';

const mandate = new MandateClient({ runtimeKey: process.env.MANDATE_RUNTIME_KEY });

try {
  const result = await mandate.validate({ action: 'transfer', reason: '...' });
} catch (error) {
  if (error instanceof CircuitBreakerError) {
    logger.error('Circuit breaker tripped: all transactions blocked');
    await notifyOwner('Circuit breaker tripped, manual reset required');
    process.exit(1);
  }
}
```

### low: Redis implementation detail may confuse application developers
- **Line(s):** 25
- **Rule:** Technical but human
- **Found:** "cached in Redis with a 30-second TTL and falls back to the database" is an internal implementation detail. Application developers do not control Redis. The relevant user-facing fact is "state change takes effect within milliseconds."
- **Suggested fix:** Keep the detail but lead with the user-facing implication: "The circuit breaker state change takes effect within milliseconds. Internally, the state is cached in Redis with a 30-second TTL..."

## Developer Experience Notes

As a developer with an agent handling real money, this page covers the most critical emergency mechanism. The two trigger types (manual and automatic) are clear. The "no auto-reset" design decision (line 19) is well-justified.

Key gaps:

1. **No webhook/notification setup.** Line 42 says "The owner receives a notification (if configured)" in the envelope-verification page context. But this page does not explain how to configure notifications. When a circuit breaker trips at 3 AM, the developer needs an alert. There should be a link to notification setup or explicit guidance on webhook configuration.

2. **No programmatic circuit breaker management example.** The API endpoints are listed (lines 33-36) but there is no curl example, no auth header, no response body. A developer cannot implement monitoring without this.

3. **No guidance on what to do after a reset.** The page says "investigate before resuming" but does not provide a runbook. What logs to check? What fields to look for? What constitutes a safe-to-resume state? For a security-critical operation, a checklist would be valuable.

4. **No discussion of partial circuit breaker.** The current design is all-or-nothing: trip = block everything. A developer running multiple transaction types might want to block only specific actions. The page should state whether this is possible or explain why all-or-nothing is the correct design.

5. **No mention of testing the circuit breaker.** A developer should test that their agent handles a tripped circuit breaker gracefully before going to production. How do you trip it in a test environment? Is there a sandbox flag?

## Score

- Critical: 0
- High: 0
- Medium: 2
- Low: 1
- **Overall:** WARN (0 critical, 0 high, has medium findings)
