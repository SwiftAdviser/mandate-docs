# QA Report: sdk/constants.mdx

## Checklist

| # | Rule | Pass/Fail |
|---|------|-----------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | FAIL (only 2 cards: /reference/chain-reference, /sdk/overview) |
| 7 | Correct terminology | PASS |
| 8 | Code examples: imports, realistic names, TS correct | PASS |
| 9 | Constants fully listed, values shown, usage example provided | PASS |

## Findings

### F1. Only 2 cross-links (lines 82-87)

The writing guide requires 3-5 cross-links. This page has only 2 cards in the Next Steps section and no inline links in the body text. Suggested additions:
- `/sdk/mandate-wallet` (uses USDC addresses and CHAIN_ID in constructor)
- `/sdk/types` (MandateWalletConfig references chainId)
- `/sdk/mandate-client` (validate example uses chain)

### F2. No "What is" opening

The page opens with "What constants does the SDK export?" which is a question-based heading (good per GEO rules) but the answer is a brief one-sentence paragraph. This is fine but could be slightly expanded to hit the 60-word self-contained answer target.

### F3. Good: Runtime key / chain mapping table (lines 49-54)

This table clearly maps key prefixes to environments and available chains. Prevents a common misconfiguration error. The warning callout on lines 56-58 reinforces it.

### F4. Good: Complete usage example (lines 62-77)

The example shows `USDC` and `CHAIN_ID` constants used in a realistic `validate()` call. Uses `process.env.MANDATE_RUNTIME_KEY!` and `String(CHAIN_ID.BASE_SEPOLIA)` which is correct since the `chain` field expects a string.

### F5. No mention of how to use constants with MandateWallet

The example only shows `MandateClient.validate()`. A `MandateWallet` constructor example using `CHAIN_ID.BASE_SEPOLIA` and `USDC.BASE_SEPOLIA` would help developers who land here from the wallet docs.

### F6. Addresses match the writing guide example values

`USDC.BASE_SEPOLIA` is `0x036CbD53842c5426634e7929541eC2318f3dCF7e`, which matches the writing guide's example value table. Consistent.

## Developer Experience Notes

- **Good:** Clean, scannable format. A developer can find any USDC address or chain ID in seconds.
- **Good:** Both code blocks and tables are provided for the same data, supporting different reading styles (scan code vs. read table).
- **Good:** The key prefix mapping section prevents the #1 misconfiguration error (testnet key with mainnet chain).
- **Gap:** Only 2 cross-links, below the 3-5 minimum.
- **Gap:** No `MandateWallet` usage example. Developers using the wallet (the more common path) only see a `MandateClient` example.
- **Minor:** The page is short (89 lines). While this is appropriate for a constants reference, adding the MandateWallet example and one more cross-link would fill it out without padding.

## Score

**7.5 / 10** -- Functionally complete for its purpose, but below the minimum cross-link threshold (2 vs. 3-5 required). Missing a MandateWallet usage example limits its usefulness for the primary SDK path. The runtime key mapping section is a valuable addition.
