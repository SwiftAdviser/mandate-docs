# Test Report: Snippet install-cli

**File:** snippets/install-cli.mdx
**Date:** 2026-03-26
**Status:** PASS
**Imported by:** guides/register-agent.mdx

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Correct terminology | PASS | No terminology violations |
| Code examples quality | PASS | Correct package `@mandate.md/cli`, shows both npx and global install |
| Self-contained | PASS | Provides two approaches (npx, global install) with no context dependencies |
| Consistent with importers | PASS | register-agent.mdx imports it but does not render it inline with `<InstallCli />` in the visible page body. The snippet is imported for availability. No inconsistency. |

## Findings

No issues found. The snippet shows the recommended `npx` approach first (no install needed), followed by global install tabs for bun and npm. This matches the writing guide principle of stating the recommended approach first.

Minor observation: only bun and npm tabs are shown for global install (no pnpm), while install-sdk.mdx includes pnpm. This is acceptable since CLI tools are typically installed globally with npm or bun, and pnpm global installs are less common. However, for consistency with install-sdk.mdx, adding a pnpm tab could be considered.

Only 1 page imports this snippet, which is low. Consider importing it in quickstart.mdx or sdk/overview.mdx if CLI installation instructions appear there.

## Score

7/7 checks passed. No action needed.
