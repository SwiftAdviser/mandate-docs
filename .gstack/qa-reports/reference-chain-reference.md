# QA Report: Chain Reference

**File:** `/reference/chain-reference.mdx`
**Date:** 2026-03-26
**Status:** PASS (minor)

## Checklist

| # | Rule | Pass |
|---|------|------|
| 1 | Frontmatter: title, sidebarTitle, description | YES |
| 2 | No em dashes (U+2014) | YES |
| 3 | No filler words | YES |
| 4 | Short paragraphs (2-4 sentences) | YES |
| 5 | "Next Steps" CardGroup at bottom | YES |
| 6 | 3-5 cross-links | PARTIAL (2 cards) |
| 7 | Correct terminology | YES |
| 8 | Tables complete and scannable | YES |

## Findings

- **Line 74: Only 2 Next Steps cards.** The writing guide requires 3-5 cross-links. Currently links to /sdk/constants and /security/credential-management. Consider adding a third card, e.g., /quickstart or /guides/register-agent.

Everything else is clean:

- Line 4: Description includes "chain IDs, USDC contract addresses, and runtime key prefixes." Keyword-rich.
- Line 9: Opening sentence with specific number: "4 EVM chains: 2 mainnets and 2 testnets."
- Lines 11-16: Main chain table. 5 columns: Chain, Chain ID, USDC Address, Decimals, Key Prefix. All 4 chains documented. Addresses are checksummed.
- Lines 20-25: Test vs live keys section. Clear enforcement rules.
- Lines 31-45: SDK constants code example with imports. Shows both CHAIN_ID and USDC namespaces.
- Lines 49-56: Default RPCs table. 4 chains with public RPC URLs.
- Lines 58-60: Tip callout recommending dedicated RPC providers for production.
- Lines 62-70: Getting started on testnet. 3-step quick start.

## Developer Experience Notes

Good. The main chain table at line 11 is the core lookup: a developer needing the Base Sepolia USDC address finds it in one scan. The SDK constants section at line 31 gives them the programmatic way to avoid hardcoding those same values.

The "Test vs live keys" section at line 20 clearly explains the enforcement: "A test key cannot validate transactions on mainnet." This prevents a common gotcha.

The "Getting started on testnet" section at line 62 is a nice touch for a reference page. It gives developers a concrete path from reading the table to actually using those values.

The only structural issue is the 2-card Next Steps (should be 3-5). This is a minor fix.

## Score

**8.5/10**
