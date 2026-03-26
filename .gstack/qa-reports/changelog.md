# Test Report: Changelog

**File:** changelog.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Changelog" |
| Frontmatter: sidebarTitle | PASS | "Changelog" |
| Frontmatter: description | PASS | "Version history and release notes for Mandate API and SDK." |
| No em dashes | PASS | No U+2014 characters found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | Entries are concise, bullet-point driven |
| Next Steps CardGroup | FAIL | No "Next Steps" CardGroup at the bottom of the page |
| Cross-links (3-5) | FAIL | count: 0. No internal cross-links to other docs pages |
| Correct terminology | PASS | "preflight" usage on lines 16, 29, 35 is in the context of explaining the alias and migration, which the writing guide explicitly allows |
| Code examples quality | N/A | No code examples (appropriate for a changelog) |
| Developer clarity | WARN | Missing links to migration guides or affected pages |

## Findings

### medium: Missing "Next Steps" CardGroup at bottom

- **Line(s):** 56 (end of file)
- **Rule:** Page structure (every page must have "Next Steps" CardGroup)
- **Found:** Page ends abruptly after v0.1.0 content
- **Fix:** Add a Next Steps CardGroup. Suggested cards: "Quickstart" (/quickstart) for getting started with the latest version, "How It Works" (/how-it-works) for understanding the current validation flow, "SDK Reference" (/sdk/overview) for the current API surface, "Migration from v0.1.0" or "Handle Errors" (/guides/handle-errors) for updated error types.

### medium: No cross-links to related documentation pages

- **Line(s):** 1-56
- **Rule:** Cross-linking (3-5 links per page)
- **Found:** Zero internal doc links. Changelog entries reference features but do not link to the pages that document them.
- **Fix:** Add inline links to relevant pages. Examples:
  - Line 15: link `POST /api/validate` to `/api-reference/endpoint/post-apivalidate`
  - Line 19: link "CLI `scan` command" to `/guides/codebase-scanner`
  - Line 20: link "MCP server mode" to `/integrations/mcp-server`
  - Line 24: link "Claude Code plugin" to `/integrations/claude-code`
  - Line 25: link "Prompt injection scanning" to `/security/prompt-injection` or `/concepts/reason-field`
  - Line 50: link "Policy engine" to `/concepts/policy-engine`

### low: v0.2.0 opening paragraph is 3 sentences but the third is long

- **Line(s):** 13
- **Rule:** Short paragraphs
- **Found:** `This makes Mandate wallet-agnostic: it works with custodial wallets (Bankr, Locus, Sponge), self-custodial signers, and any chain format.`
- **Fix:** Acceptable. The sentence is informational and reads well despite its length.

## Developer Experience Notes

As a developer, the changelog is functional but could be more helpful. The v0.2.0 breaking changes section (lines 27-31) is critical information, and the migration section (line 35) gives the exact code change needed, which is good. However, the changelog is disconnected from the rest of the documentation. If I am upgrading from v0.1.0, I would want direct links to the updated pages for each changed feature. For example, the bullet about the new `POST /api/validate` endpoint (line 15) should link to the validate endpoint docs. The Claude Code plugin bullet (line 24) should link to `/integrations/claude-code`. Without these links, a developer reading the changelog has to manually search for the updated documentation. The page would also benefit from a "Next Steps" section that guides developers to the current quickstart or migration resources.

## Score

- Critical: 0, High: 0, Medium: 2, Low: 1
- **Overall:** WARN
