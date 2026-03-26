# QA Report: sdk/mandate-wallet.mdx

## Checklist

| # | Rule | Pass/Fail |
|---|------|-----------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (4 cards in Next Steps) |
| 7 | Correct terminology | PASS ("emergency-stopped" in code string line 342 is acceptable in explanations) |
| 8 | Code examples: imports, realistic names, TS correct | PASS |
| 9 | Method signatures complete, params documented, return types shown | FAIL (partial gaps) |

## Findings

### F1. Missing `<InstallSdk />` snippet (no Installation section)

Unlike `overview.mdx` and `mandate-client.mdx`, this page has no Installation section and does not import the install snippet. A developer landing here directly (via search or deep link) has no install instructions. Should add:

```mdx
import InstallSdk from "/snippets/install-sdk.mdx";
## Installation
<InstallSdk />
```

### F2. `sendEth()` missing parameter table (lines 114-124)

The `sendEth` method has only an example but no parameter table. The `opts` parameter is not documented (does it accept `reason`? `waitForConfirmation`?). A developer has to infer from the example.

### F3. `sendTransaction()` missing return type (lines 126-155)

`sendTransaction()` documents parameters but does not state the return type. It likely returns `TransferResult`, but this is not specified. A developer must guess or check the types page.

### F4. `sendTransactionWithApproval()` missing return type (lines 157-187)

Same issue: no explicit return type stated. The example shows destructured result, but the interface is not named.

### F5. `transferWithApproval()` missing parameter table (lines 189-208)

Says "Accepts the same `opts` as `sendTransactionWithApproval`" but does not list the core parameters (`to`, `rawAmount`, `tokenAddress`). Method signature not shown.

### F6. `x402Pay()` missing return type details (lines 210-234)

Returns "the final `Response` object" but does not specify that this is a `globalThis.Response` (Fetch API). Could confuse developers unfamiliar with the pattern.

### F7. `preflightTransfer()` uses "preflight" in method name (line 236)

This is the actual SDK method name, so it must be documented as-is. However, the prose on line 238 says "Lightweight policy check" which correctly avoids "preflight" in description. Well handled.

### F8. Missing inline cross-links in body text

The page has 4 cards in Next Steps, but only the error handling section links to the errors page implicitly. No inline links to `/sdk/types` for `TransferResult`, `/sdk/intent-hash` for hash computation, or `/sdk/constants` for `USDC` addresses used in examples. The writing guide says "Use inline links in text and card groups at the bottom."

### F9. `ExternalSigner` well documented (lines 269-323)

The ethers.js wrapper example is practical and shows a real integration pattern. This is a strong section.

## Developer Experience Notes

- **Excellent:** Two constructor variants (private key vs external signer) are clearly separated with examples. A developer immediately knows which path applies to them.
- **Excellent:** The `ExternalSigner` ethers.js example is production-quality and solves a real integration problem.
- **Good:** The `transfer()` method documents the raw amount convention with a clear warning callout.
- **Gap:** `sendEth`, `sendTransaction`, `sendTransactionWithApproval`, and `transferWithApproval` are under-documented compared to `transfer()`. Missing parameter tables and return types force developers to guess or check source.
- **Gap:** No installation section. Developers arriving from search engines hit a reference page with no setup path.
- **Gap:** The `x402Pay` method is documented but there is no mention of what happens if the server does not return the expected `X-Payment-Required` header format, or if the payment fails.
- **Minor:** The `wallet.address` property (line 57-63) documents a throw condition ("throws until the address is resolved") but does not show how to handle it or what error is thrown.

## Score

**7.5 / 10** -- Strong in structure and the constructor/ExternalSigner sections. However, several methods lack complete documentation (no return types, missing parameter tables). Missing installation snippet. The gap between the thoroughly documented `transfer()` and the thinly documented `sendEth`/`sendTransaction` methods creates an uneven developer experience.
