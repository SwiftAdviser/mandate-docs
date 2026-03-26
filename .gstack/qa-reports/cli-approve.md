# QA Report: cli/approve.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PARTIAL |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 2 (frontmatter title)**: Title is "Approve", not "mandate approve". Same pattern break as event and status.
- **Line 9**: Opening explains the blocking behavior: "It blocks until the intent is approved, rejected, or the timeout expires." Critical detail for developers building pipelines.
- **Line 28**: Default timeout is 3600 seconds (1 hour). Clearly documented with explanation.
- **Line 32-51**: Two output examples (approved, expired). Both show the `feedback` field with human-readable messages.
- **Line 53-65**: "When to use this" section includes the full JSON response from validate that triggers the approval flow. Good: a developer sees the trigger and the handler on the same page.
- **Line 67-68**: Notification channels (dashboard, Slack, Telegram) mentioned. Sets expectations about the human side of the flow.
- **Line 71-76**: "Typical flow" numbered list ties approve into the full lifecycle. Steps 1-4 are clear.
- **Line 78-79**: Tip about timeout tuning is practical. Links the timeout to the server-side TTL.

## Developer Experience Notes

- **Blocking behavior is clear**: The page explicitly states that `approve` blocks. A developer building an async agent knows to handle this (run in a thread, set a short timeout, etc.).
- **Typical flow section**: Shows exactly where `approve` fits. Steps 1-4 are a complete recipe.
- **Missing**: No example of the `rejected` state output. Lines 42-51 show "expired" but not "rejected". A developer needs to distinguish these in their error handling.
- **Missing**: No mention of what happens if the intentId does not exist or is already confirmed. Error path missing.

## Score

**8/10**

Well-structured page. The blocking behavior, timeout guidance, and typical flow are excellent. Missing rejected output example and error cases. Title inconsistency.
