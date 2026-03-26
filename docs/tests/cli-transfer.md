# QA Report: cli/transfer.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 4**: Description uses "Preflight mode by default, raw mode for legacy self-custodial flows." Consistent with validate page's usage.
- **Line 9**: Opening explains that `transfer` is a convenience wrapper around `validate`. Sets the right mental model.
- **Line 20-28**: Options table is complete. All four required flags clearly marked.
- **Line 30-38**: Raw mode flags table includes defaults and required markers. Clean layout.
- **Line 54-59**: Success output matches the validate page's format. Consistent.
- **Line 62-70**: Blocked output shown. Good.
- **Line 72**: "If approval is required, the output includes the intentId and a next field pointing to mandate approve." One sentence, no example. The validate page shows the full approval JSON. Inconsistent depth.
- **Line 76-78**: Deprecated callout for raw mode. Matches the pattern from validate page.
- **Line 80**: Raw mode explanation mentions `intentHash` computation and `transfer(address,uint256)` calldata encoding. Useful technical detail.
- **Line 114**: "Sign the unsignedTx with your private key, broadcast it, then post the txHash with mandate event." Clear next step.

## Developer Experience Notes

- **Relationship to validate is clear**: Line 9 says "convenience wrapper." I know when to use `transfer` vs `validate`.
- **Raw mode output (lines 95-112)**: Shows the full `unsignedTx` object. A developer building a self-custodial flow gets everything they need: the encoded calldata, gas params, and the exact `next` command.
- **Missing**: The approval-required scenario (line 72) gets one sentence with no JSON example. A developer hitting this case for the first time on the `transfer` page (not `validate`) won't see what the output looks like.
- **Missing**: No error example for invalid token symbol or missing flags.

## Score

**8/10**

Good page. The approval-required case deserves a JSON example like the validate page has. Otherwise consistent and complete.
