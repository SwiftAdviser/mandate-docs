# Test Report: Snippet approval-flow

**File:** snippets/approval-flow.mdx
**Date:** 2026-03-26
**Status:** WARN
**Imported by:** guides/handle-approvals.mdx, guides/validate-transactions.mdx

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Correct terminology | PASS | Uses "intent" (not transaction request), "dashboard" (not admin panel) |
| Code examples quality | PASS | Full imports shown, realistic amount (`'5000'`), descriptive reason, polling with options |
| Self-contained | PASS | Opens with H3 heading, explanatory paragraph, full code block, and closing paragraph with cross-links |
| Consistent with importers | WARN | See findings below |

## Findings

### 1. Heading level concern (minor)

The snippet uses `### Handling approval workflows` (H3). This works in both importing pages because they render it inside sections where H3 is contextually appropriate. However, if imported into a page where the surrounding heading level is H2, the H3 would appear as a subsection under whatever H2 precedes it, which may not be the intended hierarchy. This is acceptable for the current importers but limits flexibility.

### 2. Cross-link to possibly non-existent pages

The closing paragraph links to `[Approvals Dashboard](/dashboard/approvals)` and `[Notifications](/dashboard/notifications)`. These paths should be verified. If these dashboard pages do not exist yet, the links will 404. The guides/handle-approvals.mdx page also links to these paths, so consistency is maintained, but broken links affect both the snippet and its importers.

### 3. Minor ordering difference with handle-approvals.mdx

The snippet shows a basic approval flow pattern. The handle-approvals.mdx page then provides a more detailed version in its own code block (with `onPoll` logging "Waiting..." instead of just "Status:"). The two code examples are consistent in structure but use slightly different log messages. This is fine since the snippet serves as the introduction and the page body expands on it.

## Score

6/7 checks passed, 1 WARN. The heading-level coupling and unverified cross-links are minor concerns.
