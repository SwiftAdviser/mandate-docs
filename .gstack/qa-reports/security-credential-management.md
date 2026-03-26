# Test Report: Credential Management

**File:** /Users/krutovoy/Projects/mandate-docs/security/credential-management.mdx
**Section:** security
**Date:** 2026-03-26
**Status:** WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Credential Management" |
| Frontmatter: sidebarTitle | PASS | "Credentials" |
| Frontmatter: description | PASS | One sentence, action-oriented |
| No em dashes (U+2014) | PASS | None found |
| No filler words | PASS | None found |
| Active voice / present tense | PASS | Consistent |
| Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit |
| "Next Steps" CardGroup at bottom | FAIL | CardGroup at line 62, no "## Next Steps" heading |
| 3-5 cross-links | PASS | 3 cards: register-agent, chain-reference, dashboard/agents |
| Concept opens with "What is X?" | PASS | Line 7 defines runtime key in first sentence |
| Code examples: imports | WARN | Bash examples (lines 14, 20-21) but no SDK code showing key usage |
| Code examples: realistic names | PASS | Uses `MANDATE_RUNTIME_KEY`, `mndt_live_abc123...` |
| Terminology: "runtime key" | PASS | Used consistently throughout, never "API key" |
| Terminology: "validate" | PASS | Not used on this page |
| Terminology: "policy engine" | PASS | Not mentioned by name |
| Terminology: "dashboard" | PASS | Used correctly (lines 13, 43, 45) |
| Terminology: "circuit breaker" | PASS | Used correctly (line 58) |
| Question-based headings | PASS | All H2s are questions |
| Self-contained answer blocks | PASS | Each section stands alone |
| Specific numbers | PASS | 2 key prefixes, 2 environments |

## Findings

### medium: Missing "## Next Steps" heading above CardGroup
- **Line(s):** 62
- **Rule:** Page Structure: "Next Steps" card group at the bottom
- **Found:** CardGroup at line 62 with no heading
- **Suggested fix:** Add `## Next Steps` heading on line 61

### medium: No SDK code example showing key initialization
- **Line(s):** 14
- **Rule:** Code Examples: show imports
- **Found:** Only bash `export` and `chmod` commands shown. No TypeScript or Python example showing how the key is loaded and used with the SDK.
- **Suggested fix:** Add a CodeGroup after the bash examples:
```typescript
import { MandateClient } from '@mandate.md/sdk';

// Load from environment variable (recommended)
const mandate = new MandateClient({
  runtimeKey: process.env.MANDATE_RUNTIME_KEY,
});
```
```python
import os
from mandate import MandateClient

mandate = MandateClient(runtime_key=os.environ["MANDATE_RUNTIME_KEY"])
```

### medium: Key rotation section lacks code example
- **Line(s):** 42-48
- **Rule:** Code Examples: show imports, realistic names
- **Found:** API endpoint `POST /api/agents/{agentId}/regenerate-key` is mentioned inline but not shown as a proper code example. No curl example, no auth header, no response body.
- **Suggested fix:** Add a curl example:
```bash
curl -X POST https://app.mandate.md/api/agents/agent_abc123/regenerate-key \
  -H "Authorization: Bearer <dashboard-session-token>" \
  -H "Content-Type: application/json"
```
With the response:
```json
{
  "runtimeKey": "mndt_live_new_key_here..."
}
```

### low: No mention of secrets management tools
- **Line(s):** 9-28
- **Rule:** Security-specific: mitigations actionable
- **Found:** Key storage advice is basic (env vars, chmod 600). No mention of production-grade secrets management: AWS Secrets Manager, HashiCorp Vault, GCP Secret Manager, Kubernetes secrets, Docker secrets.
- **Suggested fix:** Add a `<Tip>` callout after line 28: "For production deployments, use a secrets manager (AWS Secrets Manager, HashiCorp Vault, or your cloud provider's equivalent) instead of environment variables or files."

## Developer Experience Notes

As a developer running an agent with real money, credential management is foundational. This page covers the basics well: storage, prefixes, rotation, and compromise response. The key prefix table (lines 32-38) is clear.

Key gaps:

1. **No key scoping beyond environment.** The prefix table shows test vs. live, but can keys be scoped to specific actions? Specific addresses? A developer managing multiple agents wants least-privilege keys. If this is not supported, the page should say so explicitly.

2. **No automated rotation guidance.** The rotation section (lines 42-48) describes manual rotation. For production agents, key rotation should be automated on a schedule. The page does not mention rotation frequency recommendations or automation patterns.

3. **"Plan for a brief downtime window" (line 48) is concerning.** For a production agent, any downtime means missed transactions. The page mentions "hot-swapping" but does not explain how to implement it. A zero-downtime rotation guide would be valuable.

4. **No rate limiting or anomaly detection on keys.** If a compromised key is used to submit many transactions, is there rate limiting? Does Mandate detect unusual patterns? The page focuses on manual compromise response but does not discuss automated detection.

5. **Cross-link gap.** The page links to register-agent, chain-reference, and dashboard/agents. It should also link to the circuit-breaker page (mentioned at line 58) and the threat-model page for context on how key compromise fits into the broader threat landscape.

6. **Private key vs. runtime key confusion.** The page focuses on runtime keys (Mandate API auth) but line 60 mentions "the agent's private key." A developer might confuse these two credentials. A brief note distinguishing them would help: "The runtime key authenticates API calls to Mandate. The agent's private key signs blockchain transactions. These are separate credentials with different security requirements."

## Score

- Critical: 0
- High: 0
- Medium: 3
- Low: 1
- **Overall:** WARN (0 critical, 0 high, has medium findings)
