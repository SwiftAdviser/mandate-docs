# QA Report: integrations/goat-sdk.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards -- minimum threshold) |
| 7 | Terminology compliance | PASS |
| 8 | Install command shown | PASS (line 16) |
| 9 | Configuration steps clear | PASS (config table lines 56-61) |
| 10 | Code example complete | PASS (lines 23-41, shows imports and config) |
| 11 | Tools/actions table present | PASS (lines 47-50) |

## Findings

No violations found.

- Line 16: Uses `bun add` which is consistent with the project's preference (bun for TS). Good.
- Line 43: "Pass the plugin to your GOAT agent's plugin list." This instruction is vague. The code example (lines 23-41) stops at creating the plugin instance but does not show how to wire it into a GOAT agent. A developer unfamiliar with GOAT would need to look elsewhere for the agent initialization step.
- Lines 67-75: Error handling section shows both policy block and approval required messages. However, no actual try/catch code is shown. The examples are comments, not runnable code.
- Line 75: Cross-reference to `@mandate.md/sdk` for structured errors is helpful.
- Lines 56-61: Configuration table includes types, required flags, and defaults. Clean.

## Developer Experience Notes

Good page, but the code example has a gap. The snippet (lines 23-41) creates `mandatePlugin` but never shows how to pass it to a GOAT agent. A developer would need to write something like:

```typescript
const agent = getOnChainTools({ wallet: walletClient, plugins: [mandatePlugin] });
```

This missing step means the example is not fully copy-paste runnable. For a developer new to GOAT, this is a real friction point.

The error handling section (lines 64-75) explains the pattern well but does not show actual code for catching errors, only comments describing the error strings. A try/catch block or tool result check would strengthen this.

Cross-links are at the minimum (3). Adding a link to `/guides/validate-transactions` or `/sdk/errors` would improve navigation.

## Score

**7.5 / 10**
