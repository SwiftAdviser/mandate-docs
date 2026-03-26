# QA Report: integrations/acp-virtuals.mdx

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
| 8 | Install command shown | PASS (line 13) |
| 9 | Configuration steps clear | PARTIAL -- see findings |
| 10 | Code example complete | PASS (lines 22-41) |
| 11 | Tools/actions table present | PASS (methods table lines 58-64, exports table lines 68-72) |

## Findings

- **Line 25**: `acpApiKey: process.env.ACP_API_KEY!` -- The parameter is named `acpApiKey`. The writing guide mandates "runtime key" not "API key" for Mandate credentials, but this is ACP's own credential, not Mandate's. The Mandate credential is correctly named `mandateRuntimeKey` (line 26). No violation, but worth noting the distinction is clear.
- **Line 72**: `MandateAcpConfig` type lists `acpApiKey` and `mandateRuntimeKey` plus optional `mandateApiUrl` and `acpApiUrl`. No dedicated configuration table with types, required flags, and defaults. The exports table partially fills this role, but a formal configuration parameters table (like other integration pages have) is missing.
- Lines 46-55: The 6-step validation flow explanation is excellent. Clear numbered list showing how USD amounts become synthetic USDC transfers for policy validation.
- Line 17: "No additional peer dependencies." Clear and helpful.

## Developer Experience Notes

The page explains a non-obvious concept well: ACP payments go through a smart wallet, so Mandate creates a "synthetic" ERC20 transfer to validate the USD spend amount. The 6-step flow (lines 49-55) makes this transparent.

Key gap: there is no formal configuration table with types and required flags. The GOAT, AgentKit, ElizaOS, and GAME pages all have one. A developer comparing integration options will notice this inconsistency. The exports table (lines 68-72) lists the config type but does not break down its fields.

The code example (lines 22-41) is complete and shows both the happy path and the block path in a single snippet. This is good. However, there is no error handling section showing what happens when the Mandate API is unreachable or when approval is required. Other integration pages cover these cases.

Missing: no mention of error handling patterns (other pages show policy block and approval required responses). A developer needs to know what `createAndPay` returns or throws on network errors.

## Score

**7 / 10**
