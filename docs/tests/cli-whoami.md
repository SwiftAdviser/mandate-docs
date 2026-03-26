# QA Report: cli/whoami.mdx

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
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 6 (cross-links)**: Only 2 cards in Next Steps. Needs at least 1 more. Suggested: `/cli/activate` (since whoami verifies activate worked) or `/cli/overview`.
- **Line 9**: Opening sentence lists three use cases ("verify that login worked, check which agent is active, or confirm the wallet address"). Good.
- **Line 17-24**: Output JSON is realistic and matches the field descriptions table.
- **Line 27-33**: Field descriptions table is thorough. The `keyPrefix` row explains test vs live key distinction, which is valuable.
- **Line 35**: "The `keyPrefix` tells you whether you are using a test or live key." This is a standalone sentence paragraph. Slightly redundant with the table row, but acceptable as reinforcement.
- **Line 37-39**: Tip callout is practical: run whoami after login and after activate.

## Developer Experience Notes

- **Clear and useful**: I know exactly what whoami returns and when to use it. The field table removes all ambiguity.
- **Missing**: No mention of what happens when credentials are missing or corrupted. A developer running `whoami` as a smoke test needs to know the failure mode.
- **Missing**: No `--json` or formatting flags. If the output is always JSON, that is fine, but worth stating explicitly: "Output is always JSON."

## Score

**7/10**

Clean page, easy to follow. Below cross-link minimum (2 vs 3 required). No error output shown.
