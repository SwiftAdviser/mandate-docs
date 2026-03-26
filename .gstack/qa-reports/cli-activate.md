# QA Report: cli/activate.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | FAIL (only 2 cards, no inline links) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PARTIAL |

## Findings

- **Line 6 (cross-links)**: Only 2 cards in Next Steps. Writing guide requires 3-5 cross-links. Missing at least one more. Suggested additions: link to `/guides/register-agent` (registration guide) or `/cli/overview` (back to full command list).
- **Line 9**: Good opening, but "sets the wallet address for an agent that was registered without one" implies this command cannot change an existing address. Is that true? If you can update the address, the description should say so.
- **Line 17**: "When to use it" section is helpful context, but it only covers the zero-address case. Does not mention whether you can re-activate with a different address.
- **Line 26-33**: Output example is clear. The `onboardingUrl` field appears here but not in the login output. No explanation of what it is or how it differs from `claimUrl`.
- **Line 37-39**: Note about requiring authentication is important. Placed well.

## Developer Experience Notes

- **Page is short**: 50 lines. That is fine for a simple command, but the gaps hurt more on a short page.
- **Missing**: No flags table. The command takes a positional argument (`0xYourWalletAddress`), but there is no "Arguments" table like `event`, `status`, and `approve` have. Inconsistent with sibling pages.
- **Missing**: No error output. What if I pass an invalid address? What if I haven't logged in?
- **Missing**: The `onboardingUrl` in the output (line 32) is unexplained. A developer will wonder what to do with it.

## Score

**6/10**

Below the required cross-link count. Missing arguments table, error examples, and `onboardingUrl` explanation. The shortest CLI page but has the most gaps proportionally.
