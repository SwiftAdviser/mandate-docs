# Test Report: Prompt Injection Detection

**File:** /Users/krutovoy/Projects/mandate-docs/security/prompt-injection.mdx
**Section:** security
**Date:** 2026-03-26
**Status:** WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Prompt Injection Detection" |
| Frontmatter: sidebarTitle | PASS | "Prompt Injection" |
| Frontmatter: description | PASS | One sentence, action-oriented |
| No em dashes (U+2014) | PASS | None found |
| No filler words | PASS | None found |
| Active voice / present tense | PASS | Consistent |
| Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit |
| "Next Steps" CardGroup at bottom | FAIL | CardGroup exists (line 89) but no "## Next Steps" heading |
| 3-5 cross-links | PASS | 3 cards: reason-field, block-reasons, threat-model |
| Concept opens with "What is X?" | PASS | Line 7 defines prompt injection in first sentence |
| Code examples: imports | N/A | JSON response example only (line 70-76), no SDK code |
| Code examples: realistic names | PASS | JSON example uses realistic blockReason values |
| Terminology: "runtime key" | PASS | Not mentioned |
| Terminology: "validate" | PASS | Uses "validate()" correctly (line 11) |
| Terminology: "preflight" | WARN | Line 11 uses "preflight()" which is acceptable since it's naming the actual API method, not substituting for "validate" |
| Terminology: "policy engine" | PASS | Used correctly at line 11 |
| Terminology: "block reason" | PASS | Uses "blockReason" in JSON (line 74) |
| Terminology: "dashboard" | PASS | Not mentioned |
| Terminology: "circuit breaker" | PASS | Not mentioned |
| Question-based headings | PASS | All H2s are questions |
| Self-contained answer blocks | PASS | Each section is independently citable |
| Specific numbers | PASS | "18+ regex patterns", "two layers" |

## Findings

### medium: Missing "## Next Steps" heading above CardGroup
- **Line(s):** 89
- **Rule:** Page Structure: "Next Steps" card group at the bottom
- **Found:** CardGroup at line 89 has no heading above it
- **Suggested fix:** Add `## Next Steps` on line 88

### medium: No SDK code example showing how to handle a prompt injection block
- **Line(s):** 70-76
- **Rule:** Code Examples: show imports, realistic names
- **Found:** Only a raw JSON response is shown. No TypeScript/Python example demonstrating how a developer catches a `reason_blocked` response in their agent code.
- **Suggested fix:** Add a CodeGroup showing how to detect and handle a `reason_blocked` response:
```typescript
import { MandateClient } from '@mandate.md/sdk';

const mandate = new MandateClient({ runtimeKey: process.env.MANDATE_RUNTIME_KEY });
const result = await mandate.validate({ action: 'transfer', reason: userInput });

if (!result.allowed && result.blockReason === 'reason_blocked') {
  logger.warn('Prompt injection detected', { declineMessage: result.declineMessage });
  // Do NOT retry with modified reason: this is likely an attack
}
```

### low: "guard_rules" terminology not explained
- **Line(s):** 84
- **Rule:** Technical but human, no unexplained jargon
- **Found:** "Adjust guard_rules in the policy" references a field name without explaining what guard_rules is or linking to its documentation.
- **Suggested fix:** Add inline link: "Adjust `guard_rules` in the [policy builder](/dashboard/policy-builder)"

### low: Venice.ai dependency mentioned without context
- **Line(s):** 48
- **Rule:** Self-contained answer blocks
- **Found:** "The judge runs on Venice.ai with zero data retention" introduces a third-party dependency without explaining what Venice.ai is or linking to it.
- **Suggested fix:** Add brief context: "Venice.ai, a privacy-focused LLM inference provider" or link to their docs.

## Developer Experience Notes

As a developer running an agent with real money, this page answers the critical question: "How does Mandate stop my agent from being tricked into draining its wallet?" The pattern categories (lines 19-43) are concrete and helpful. The LLM judge explanation (lines 48-56) is transparent about the architecture.

Key gaps:

1. **No guidance on testing.** A developer wants to test that their agent's reasons pass the scanner before going to production. There is no mention of a test endpoint, sandbox mode, or example reasons that would/would not trigger the scanner. For a security feature, testability is essential.

2. **Counter-evidence (lines 60-64) is powerful but underspecified.** The `context` field is mentioned but there is no code example, no list of what constitutes "strong context," and no clarity on the severity hierarchy. A developer cannot implement this without guessing.

3. **"18+ patterns" is vague on purpose** (to avoid teaching attackers), which is reasonable. But the page should explicitly state this is intentional: "The full pattern list is not published to avoid adversarial adaptation."

4. **No latency impact discussion.** The LLM judge adds latency. A developer handling time-sensitive transactions needs to know: how much latency does the two-layer scanner add? Is it 50ms? 500ms? 2 seconds? This affects architecture decisions.

5. **False positive handling (lines 81-87) is good** but does not mention monitoring. A developer needs to know how to set up alerts for `reason_blocked` events to catch both real attacks and false positives.

## Score

- Critical: 0
- High: 0
- Medium: 2
- Low: 2
- **Overall:** WARN (0 critical, 0 high, has medium findings)
