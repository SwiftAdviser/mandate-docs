# Writing Guide for Mandate Documentation

This is the style guide every article follows. Use it when writing new pages or reviewing existing ones.

## Voice and Tone

- **Direct.** Second person ("you"). Active voice. Present tense.
- **Concise.** Short paragraphs: 2-4 sentences max.
- **No em dashes.** Use colons, periods, or commas instead.
- **No filler words.** Never use "simply", "just", "easily", "leverage", "utilize", "seamlessly", "robust".
- **Opinionated.** State the recommended approach first. Alternatives second. Deprecated last.
- **Technical but human.** No marketing superlatives. No buzzwords.

## Page Structure

Every page must have:

1. **Frontmatter** with `title`, `sidebarTitle`, `description`
2. **Content** with 3-5 cross-links to related pages
3. **"Next Steps" CardGroup** at the bottom

```mdx
---
title: "Page Title"
sidebarTitle: "Sidebar Label"
description: "One sentence. Action-oriented. Include target keywords."
---

## Content here

<CardGroup cols={2}>
  <Card title="Related Page" icon="arrow-right" href="/path/to/page">
    One-line description.
  </Card>
</CardGroup>
```

## Code Examples

- Always show imports
- Use realistic variable names (`runtimeKey`, not `key` or `foo`)
- Show both success and error paths
- Code tabs order: TypeScript SDK, CLI, curl

### Standard example values

| Value | Use |
|-------|-----|
| `mndt_test_abc123...` | Runtime key (never real keys) |
| `0x036CbD53842c5426634e7929541eC2318f3dCF7e` | USDC on Base Sepolia |
| `0xRecipientAddress` | Destination address |
| `84532` | Chain ID (Base Sepolia) |
| `5000000` | 5 USDC (6 decimals) |

## Terminology

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
| circuit breaker | kill switch (acceptable in explanations only) |

## GEO / LLM Optimization Rules

1. **Definition first**: open concept pages with "What is X?" in the first 60 words
2. **Answer blocks**: write 134-167 word self-contained passages that can be cited without context
3. **Question-based headings**: use H2/H3 that match developer search queries
4. **Comparison tables**: every "vs" opportunity gets a structured table
5. **Specific numbers**: always include concrete data ("14 validation checks", "12 blockReason values")

## Callouts

```mdx
<Note>Supplementary information.</Note>
<Warning>Security-critical rules. Fail-safe behavior. Mandatory validation.</Warning>
<Tip>Recommended patterns and best practices.</Tip>
<Info>Version info, deprecation notices, compatibility notes.</Info>
```

## Deprecated Content

Always lead with the current approach. Mark deprecated with `<Info>` callout:

```mdx
<Info>**Deprecated.** Use `validate()` instead.</Info>
```

## Snippets

7 reusable blocks in `/snippets/`:

| Snippet | Content |
|---------|---------|
| `install-sdk.mdx` | SDK install (bun/npm/pnpm tabs) |
| `install-cli.mdx` | CLI install (npx or global) |
| `error-handling.mdx` | Error class hierarchy with instanceof checks |
| `fail-safe.mdx` | 5 non-negotiable fail-safe rules |
| `reason-field.mdx` | What the reason field is and why it matters |
| `validate-response.mdx` | PreflightResult shape with field descriptions |
| `approval-flow.mdx` | ApprovalRequiredError catch + waitForApproval pattern |

Import with: `import SnippetName from "/snippets/snippet-name.mdx";`
