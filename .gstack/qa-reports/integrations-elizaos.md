# QA Report: integrations/elizaos.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline link to /dashboard/approvals) |
| 7 | Terminology compliance | PASS |
| 8 | Install command shown | PASS (line 13) |
| 9 | Configuration steps clear | PASS (env vars table lines 34-38) |
| 10 | Code example complete | PASS (lines 22-28, minimal but shows plugin registration) |
| 11 | Tools/actions table present | PASS (actions table lines 44-48, provider table lines 54-56) |

## Findings

No violations found.

- Line 9: Description says "three actions (transfer, x402Pay, sendEth) and one provider (walletStateProvider)." The actions table (lines 44-48) confirms these. Consistent.
- Lines 22-28: Usage example is minimal but complete for ElizaOS patterns. Shows import and plugin registration in `AgentRuntime`. This is the right level of detail: ElizaOS devs know what a plugin array is.
- Lines 34-38: Environment variables table is clear. Defaults documented. `MANDATE_CHAIN_ID` defaults to 84532 (Base Sepolia).
- Lines 64-72: Error handling section shows both `text` and `content` fields from callbacks. The structured `content` object is a strong detail for developers building agent logic around policy blocks.
- Line 77: Tip about `validate` method checking for env var is a good "gotcha" warning.

## Developer Experience Notes

Clean page. The ElizaOS integration is the most straightforward of the SDK integrations: import the plugin, add it to the runtime, set env vars. The code example (lines 22-28) is genuinely copy-paste ready for an ElizaOS developer.

The actions table includes "Similes" which is ElizaOS-specific terminology for action aliases. This shows the docs author understands the target framework. A developer looking for "SEND_TOKENS" will see it maps to `MANDATE_TRANSFER`.

The error handling section is thorough. Showing both the human-readable `text` and the structured `content` object lets developers choose the right approach for their agent.

Cross-links are at the minimum (3 cards). Adding a link to `/integrations/game-virtuals` or `/sdk/mandate-wallet` would help developers exploring related options.

## Score

**8.5 / 10**
