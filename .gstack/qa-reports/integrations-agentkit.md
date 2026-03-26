# QA Report: integrations/agentkit.mdx

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
| 9 | Configuration steps clear | PASS (config table lines 75-80) |
| 10 | Code example complete | PARTIAL -- see findings |
| 11 | Tools/actions table present | PASS (actions table lines 38-42, methods table lines 48-53) |

## Findings

- **Line 32**: "Pass `walletProvider` and `actions` to your AgentKit agent configuration." Same gap as the GOAT page: the code example creates the provider and actions but does not show how to wire them into an AgentKit agent. A developer needs to know what the full agent init looks like.
- **Line 67**: Link to `/dashboard/approvals` is a good inline cross-reference. However, this path may not exist as a docs page (it is a dashboard URL). Verify the link target.
- **Line 70**: Warning about `signMessage()` not being implemented is important. Good placement.
- Lines 38-42: Actions table includes 4 actions (transfer, x402_pay, get_policy, get_quota). The last two are read-only policy introspection tools, which is a nice addition not present in other plugins.
- Lines 48-53: WalletProvider methods table is clear. `getMandateWallet()` escape hatch is documented.

## Developer Experience Notes

Solid page. The two-table structure (Actions + WalletProvider methods) gives developers a clear picture of what they get from the package.

Key gap: the code example (lines 22-31) is incomplete. A developer copying this code does not see how to create an AgentKit agent with the Mandate provider. Something like:

```typescript
const agent = new AgentKit({ walletProvider, actionProviders: [actions] });
```

Would make this copy-paste ready. Without it, a developer must read AgentKit docs separately to complete the integration.

The error handling section (lines 57-65) shows string-based returns with `intentId` and `approvalId`. This is useful for understanding the pattern, but no code shows how to handle these in an agent loop.

## Score

**7.5 / 10**
