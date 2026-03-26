# QA Report: cli/status.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PARTIAL |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (2 cards + 1 inline link to /reference/intent-states = 3) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 2 (frontmatter title)**: Title is "Status", not "mandate status". Same inconsistency as the event page. Other pages use "mandate login", "mandate validate", etc.
- **Line 9**: Opening is clear. Lists three use cases: confirmed, waiting for approval, failed.
- **Line 22-35**: Output fields table is thorough. Types are shown (`string | null`). Good for programmatic consumers.
- **Line 39-76**: Three example outputs cover the main states: confirmed, approval_pending, failed. All three show realistic field values.
- **Line 74**: Failed transaction output includes `blockReason: "envelope_mismatch"`. Connects to the circuit breaker concept from the event page.
- **Line 78**: Explanation of the `next` field across different states is useful. Covers `reserved`, `approval_pending`, and `broadcasted`.
- **Line 80**: Inline link to Intent States reference. Good cross-link.

## Developer Experience Notes

- **Three output examples**: Excellent coverage. I can match my actual output against these examples to understand what happened.
- **Output fields table**: The `string | null` types help me write code that handles the response correctly. Good detail.
- **Missing**: No `--json` or `--watch` flag. If polling is needed (as suggested by "polling status again" on line 78), a `--watch` or `--poll` flag would be expected. If it does not exist, worth noting that the developer must poll manually.
- **Missing**: No mention of how often to poll, or whether the `next` field includes a suggested interval.

## Score

**8/10**

Strong reference page. Frontmatter title inconsistency. Polling guidance would help developers building automated flows.
