# Test Report: Address Risk Scanning

**File:** /Users/krutovoy/Projects/mandate-docs/security/risk-scanning.mdx
**Section:** security
**Date:** 2026-03-26
**Status:** WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Address Risk Scanning" |
| Frontmatter: sidebarTitle | PASS | "Risk Scanning" |
| Frontmatter: description | PASS | One sentence, action-oriented |
| No em dashes (U+2014) | PASS | None found |
| No filler words | PASS | None found |
| Active voice / present tense | PASS | Consistent |
| Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit |
| "Next Steps" CardGroup at bottom | FAIL | CardGroup at line 49, no "## Next Steps" heading |
| 3-5 cross-links | PASS | 3 cards: threat-model, block-reasons, policy-builder |
| Concept opens with "What is X?" | PASS | Line 7 defines address risk scanning in first sentence |
| Code examples: imports | FAIL | No code examples at all |
| Code examples: realistic names | N/A | No code |
| Terminology: "runtime key" | PASS | Not mentioned |
| Terminology: "validate" | PASS | "validation" used correctly |
| Terminology: "policy engine" | PASS | Used at lines 10, 12, 39 |
| Terminology: "block reason" | PASS | "blockReason" used in table (line 22) |
| Terminology: "dashboard" | PASS | Not mentioned |
| Terminology: "circuit breaker" | PASS | Not mentioned |
| Question-based headings | PASS | All H2s are questions |
| Self-contained answer blocks | PASS | Each section stands alone |
| Specific numbers | PASS | "10 minutes" cache, 4 risk levels |

## Findings

### medium: Missing "## Next Steps" heading above CardGroup
- **Line(s):** 49
- **Rule:** Page Structure: "Next Steps" card group at the bottom
- **Found:** CardGroup at line 49 with no heading
- **Suggested fix:** Add `## Next Steps` heading on line 48

### medium: No code examples
- **Line(s):** entire page
- **Rule:** Code Examples: show imports
- **Found:** No code showing how risk scanning results appear in a validate response or how to enable/disable it via the API.
- **Suggested fix:** Add at minimum a validate response example showing risk scanning in action:
```json
{
  "allowed": false,
  "blockReason": "aegis_critical_risk",
  "declineMessage": "Destination address flagged as critical risk by Aegis"
}
```
And an SDK example:
```typescript
import { MandateClient } from '@mandate.md/sdk';

const mandate = new MandateClient({ runtimeKey: process.env.MANDATE_RUNTIME_KEY });
const result = await mandate.validate({
  action: 'transfer',
  to: '0xSuspiciousAddress',
  reason: 'Vendor payment',
});

if (result.blockReason === 'aegis_critical_risk') {
  logger.error('Destination address is on a sanctions/scam list');
}
```

### medium: Fail-open behavior deserves a Warning callout
- **Line(s):** 38-41
- **Rule:** Security-specific: mitigations actionable
- **Found:** "the transaction proceeds with a `risk_degraded` flag" is a fail-open design. This is a deliberate and reasonable choice, but for a security page it should be highlighted with a `<Warning>` callout to ensure developers understand the implication: during Aegis downtime, transactions to sanctioned addresses could be approved.
- **Suggested fix:** Wrap lines 38-41 in a `<Warning>` component:
```mdx
<Warning>
When the Aegis service is unavailable, transactions proceed without risk screening.
A `risk_degraded` flag is added to the audit log. Monitor for this flag and review
affected transactions after service recovery.
</Warning>
```

### low: "W3A integration" not explained
- **Line(s):** 7
- **Rule:** Technical but human, no unexplained jargon
- **Found:** "(W3A integration)" is mentioned parenthetically but W3A is never explained or linked.
- **Suggested fix:** Either remove the parenthetical or add a brief explanation: "Aegis, a Web3 threat intelligence service by W3A"

## Developer Experience Notes

As a developer running an agent with real money, this page is important for understanding how Mandate protects against sending funds to malicious addresses. The risk level table (lines 17-23) is clear and actionable.

Key gaps:

1. **Fail-open behavior (lines 38-41) needs more emphasis.** If Aegis goes down and a developer's agent sends funds to a sanctioned address during the outage, the developer is still liable. The page should recommend a mitigation strategy: "Consider maintaining a local blocklist of known-bad addresses as a fallback during Aegis downtime."

2. **No guidance on monitoring risk_degraded events.** The page mentions the flag but not how to detect it. Webhook? Dashboard alert? Log grep? A developer needs an operational playbook.

3. **OFAC compliance implications.** Line 30 mentions OFAC sanctions lists. This has legal implications. The page should note that while Mandate screens against OFAC lists, compliance responsibility ultimately lies with the agent operator. A disclaimer or link to legal considerations would be appropriate.

4. **No allowlist interaction explained.** If a developer has an address on their allowlist, does the risk scanner still run? Can an allowlisted address be overridden by a CRITICAL risk flag? This interaction between two security features is not documented.

5. **Cache staleness risk.** "Results are cached per address for 10 minutes" (line 13). If an address is added to a sanctions list, there is a 10-minute window where transactions could be approved. The page should acknowledge this and explain whether there is an invalidation mechanism.

6. **No coverage guarantee.** The page lists four data source categories (lines 30-33) but does not specify which specific databases are checked. A developer doing compliance due diligence needs to know: is this Chainalysis? TRM Labs? A proprietary database?

## Score

- Critical: 0
- High: 0
- Medium: 3
- Low: 1
- **Overall:** WARN (0 critical, 0 high, has medium findings)
