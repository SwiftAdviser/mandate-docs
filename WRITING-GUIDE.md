# Mandate Docs Writing Guide

Every article in this documentation follows these rules. No exceptions.

## Voice and Tone

- **Direct.** Second person ("you"). Active voice. Present tense.
- **Concise.** Short paragraphs: 2-4 sentences max.
- **No em dashes.** Use colons, periods, or commas instead.
- **No filler words.** Never use "simply", "just", "easily", "leverage", "utilize", "seamlessly", "robust".
- **Opinionated.** State the recommended approach first. Alternatives second. Deprecated last.
- **Technical but human.** No marketing superlatives. No buzzwords.

## Page Structure

Every page follows this structure:

```mdx
---
title: "Page Title"
sidebarTitle: "Sidebar Label"
description: "One-sentence description. Action-oriented. Include target keywords."
---

{/* Optional: import snippets */}
import SnippetName from "/snippets/snippet-name.mdx";

## Content

Paragraphs, code, tables...

## Next Steps

<CardGroup cols={2}>
  <Card title="Related Page" icon="arrow-right" href="/path/to/page">
    One-line description of what they learn next.
  </Card>
  <Card title="Another Page" icon="arrow-right" href="/path/to/page">
    One-line description.
  </Card>
</CardGroup>
```

### Required elements:
- Frontmatter with `title`, `sidebarTitle`, `description`
- 3-5 cross-links to related pages
- "Next Steps" card group at the bottom

## Code Examples

- Always show imports
- Use realistic variable names (`runtimeKey`, not `key` or `foo`)
- Show both success and error paths
- Use code tabs in this order: TypeScript SDK, Python, CLI, curl

```mdx
<CodeGroup>
  ```typescript TypeScript
  import { MandateClient } from '@mandate.md/sdk';
  // ...
  ```

  ```python Python
  import os, requests
  headers = {"Authorization": f"Bearer {os.environ['MANDATE_RUNTIME_KEY']}"}
  resp = requests.post("https://app.mandate.md/api/validate", headers=headers, json={...})
  ```

  ```bash CLI
  npx @mandate.md/cli validate --action transfer --reason "..."
  ```

  ```bash curl
  curl -X POST https://app.mandate.md/api/validate \
    -H "Authorization: Bearer mndt_test_abc123" \
    -H "Content-Type: application/json" \
    -d '{"action": "transfer", "reason": "..."}'
  ```
</CodeGroup>
```

### Example values:
| Value | Use |
|-------|-----|
| `mndt_test_abc123...` | Runtime key (never real keys) |
| `0x036CbD53842c5426634e7929541eC2318f3dCF7e` | USDC on Base Sepolia |
| `0xRecipientAddress` | Destination address |
| `84532` | Chain ID (Base Sepolia) |
| `5000000` | 5 USDC (6 decimals) |

## Terminology

Always use these terms. Never the alternatives.

| Correct | Never use |
|---------|-----------|
| runtime key | API key, secret key, auth token |
| validate | preflight (unless explaining the alias) |
| intent | transaction request, tx request |
| policy engine | validation engine, rules engine |
| block reason | error reason, rejection reason |
| dashboard | admin panel, web UI, console |
| reason field | justification, rationale |
| non-custodial | self-hosted, keyless |
| circuit breaker | kill switch, emergency stop (acceptable in explanations) |

## GEO / LLM Optimization

Every page is optimized for AI citation. Follow these rules:

### 1. Definition first
Open concept pages with "What is X?" answered in the first 60 words.

```mdx
## What is the policy engine?

The Mandate policy engine evaluates every agent transaction against 14 sequential
checks: circuit breaker status, schedule windows, address allowlists, blocked actions,
per-transaction limits, daily and monthly quotas, risk screening, reputation scoring,
reason scanning, and approval thresholds. If any check fails, the transaction is
blocked with a specific `blockReason` code.
```

### 2. Self-contained answer blocks
Write 134-167 word passages that can be cited without surrounding context. Include specific numbers and claims.

### 3. Question-based headings
Use H2/H3 headings that match developer search queries:
- "How does Mandate validate transactions?"
- "What happens when the Mandate API is unreachable?"
- "How do I handle approval workflows?"

### 4. Comparison tables
Every "vs" opportunity gets a structured table:
- Session keys vs Mandate
- Custodial vs non-custodial
- Preflight vs raw validation
- SDK vs CLI vs API

### 5. Specific numbers
Always include concrete data: "14 validation checks", "12 blockReason values", "4 supported chains", "5 error classes".

## Callouts

Use Mintlify callout components:

```mdx
<Note>Supplementary information.</Note>
<Warning>Security-critical rules. Fail-safe behavior. Mandatory validation.</Warning>
<Tip>Recommended patterns and best practices.</Tip>
<Info>Version info, deprecation notices, compatibility notes.</Info>
```

## Deprecated Content

Mark with `<Info>` callout. Keep the content but always lead with the current approach:

```mdx
<Info>
  **Deprecated.** Use `validate()` instead. Raw validation is kept for legacy
  self-custodial flows but will be removed in a future version.
</Info>
```

## Snippets

Import reusable blocks from `/snippets/`:

```mdx
import InstallSdk from "/snippets/install-sdk.mdx";
import ErrorHandling from "/snippets/error-handling.mdx";
import FailSafe from "/snippets/fail-safe.mdx";
import ReasonField from "/snippets/reason-field.mdx";
import ValidateResponse from "/snippets/validate-response.mdx";
import ApprovalFlow from "/snippets/approval-flow.mdx";

<InstallSdk />
```

## Cross-Linking

Every page links to 3-5 related pages. Use inline links in text and card groups at the bottom.

Common link targets:
- Error handling: `/sdk/errors` and `/guides/handle-errors`
- Block reasons: `/reference/block-reasons`
- Intent states: `/reference/intent-states`
- Policy fields: `/reference/policy-fields`
- Chain reference: `/reference/chain-reference`
- Glossary: `/concepts/glossary`
