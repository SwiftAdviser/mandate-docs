# Test Report: Handle Approval Workflows

**File:** guides/handle-approvals.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Handle Approval Workflows" |
| Frontmatter: sidebarTitle | PASS | "Handle Approvals" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 4 cards |
| Cross-links (3-5) | PASS | count: 5+ (inline: /dashboard/policy-builder, /dashboard/approvals, /dashboard/notifications; cards: 4) |
| Correct terminology | PASS | Uses correct terminology throughout |
| Code examples quality | WARN | See findings below |
| Steps are followable | PASS | Clear flow from error catch to polling to resolution |
| Error handling shown | PASS | Shows ApprovalRequiredError handling, timeout, rejection |
| Developer clarity | PASS | Very clear developer flow |

## Findings

### Medium: CodeGroup missing Python tab

- **Line(s):** 35-76
- **Rule:** CodeGroup tab order: TypeScript SDK, Python, CLI, curl
- **Found:** CodeGroup has TypeScript, CLI, curl. Python tab is missing.
- **Fix:** Add a Python example showing how to poll for approval status using `requests.get()` with the intent ID.

### Low: MandateWallet example missing error handling

- **Line(s):** 92-116
- **Rule:** Show both success and error paths
- **Found:** The `transferWithApproval()` example shows only the success path. No try/catch for when approval is rejected or times out.
- **Fix:** Wrap in try/catch showing what happens when `status.status === 'rejected'` or when the timeout expires.

### Low: No prerequisite mention

- **Line(s):** (missing)
- **Rule:** Guides should mention prerequisites
- **Found:** No explicit mention that this guide assumes you have already set up validation (the previous guide).
- **Fix:** Add a brief note: "This guide assumes you have [validation set up](/guides/validate-transactions). Approval handling is a sub-flow of the validate() response."

## Developer Experience Notes

The guide is clear and practical. The 7 approval triggers table is immediately useful for understanding when approvals fire. The two approaches (manual with MandateClient vs automatic with MandateWallet) give developers good options. The section on how owners approve (dashboard, Telegram, Slack) fills an important gap. The TTL explanation prevents a common mistake (re-polling expired intents). As a developer, I can follow this: catch the error, extract intentId, poll, handle the decision. One gap: what happens in my agent loop while waiting? Should I block the loop, spawn a background task, or queue the intent?

## Score
- Critical: 0, High: 0, Medium: 1, Low: 2
- **Overall:** WARN
