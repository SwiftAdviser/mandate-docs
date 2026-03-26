# QA Report: sdk/mandate-client.mdx

## Checklist

| # | Rule | Pass/Fail |
|---|------|-----------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (4 cards + 2 inline links to /sdk/mandate-wallet and /reference/intent-states = 6 total) |
| 7 | Correct terminology | PASS (uses "preflight" only when documenting the alias method, which the guide allows) |
| 8 | Code examples: imports, realistic names, TS correct | PASS |
| 9 | Method signatures complete, params documented, return types shown | PASS |

## Findings

### F1. Missing `reason` parameter in `transfer()` error example (line 77)

Line 77 code: `await wallet.transfer(to, amount, tokenAddress);` -- This is in the `PolicyBlockedError` section inside the errors page content, but on the mandate-client page (line 77 reference in errors.mdx). Actually this is on the errors page, not here. No issue on this page.

### F2. `preflight()` method documented (lines 208-216)

The `preflight()` alias is documented with a clear deprecation note directing developers to `validate()`. This is the correct handling per the writing guide ("unless explaining the alias"). Well done.

### F3. `rawValidate()` properly marked deprecated (lines 219-222)

Uses the `<Info>` callout with "Deprecated" label as specified in the writing guide. Correctly leads with the current approach (`validate()`).

### F4. Excellent error handling example (lines 158-202)

The full error handling example covers all 4 error classes with realistic comments. Uses the real USDC address from the example values table. Good realistic `reason` field.

### F5. Comparison table (lines 444-456)

The MandateClient vs MandateWallet comparison table is well-structured and answers a natural developer question. Matches the writing guide's guidance on comparison tables.

### F6. No mention of rate limiting

No information about API rate limits on `validate()`, `getStatus()`, or polling methods. A developer running `waitForApproval` with a 5-second interval would want to know if there are rate limits.

### F7. `waitForApproval` default timeout (line 354)

The 1-hour default is documented and explained ("matches server approval TTL"). Good developer-facing context.

## Developer Experience Notes

- **Excellent:** Every method has a full signature, parameter table, return type interface, throws table, and working example. This is the gold standard for SDK reference docs.
- **Excellent:** The constructor is documented with both required and optional fields, with a security warning about env vars.
- **Good:** The `register()` static method clearly explains it does not need auth, which prevents confusion.
- **Good:** The `postEvent` warning about skipping it (line 292-294) prevents a common integration bug.
- **Gap:** No rate limit documentation for polling methods.
- **Gap:** No example of `waitForConfirmation` combined with `rawValidate` as a complete end-to-end flow (the example on line 432-442 starts mid-flow).
- **Minor:** The `register()` example uses `'0xYourAgentWalletAddress'` which is not a valid hex address. The writing guide prefers `0xRecipientAddress` style, but for a wallet address, something like `'0xAgentWalletAddress'` would be more consistent.

## Score

**9.0 / 10** -- Comprehensive reference page. Every method is fully documented with signatures, params, return types, error classes, and examples. The comparison table and sub-path import section add value. Missing rate limit info and one incomplete end-to-end example are the only gaps.
