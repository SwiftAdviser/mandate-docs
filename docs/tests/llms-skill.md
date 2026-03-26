# Test Report: Mandate SKILL Reference

**File:** llms-skill.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Mandate SKILL Reference" |
| Frontmatter: sidebarTitle | PASS | "SKILL.md (for AI agents)" |
| Frontmatter: description | PASS | Clear, action-oriented |
| No em dashes | PASS | No U+2014 characters found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | Extremely concise throughout, as appropriate for machine-readable reference |
| Next Steps CardGroup | FAIL | No "Next Steps" CardGroup at the bottom of the page |
| Cross-links (3-5) | PASS | count: 12+ (extensive internal linking to guides, references, and integration pages) |
| Correct terminology | PASS | Uses "runtime key", "dashboard", "block reason", "circuit breaker", "reason field", "non-custodial" correctly throughout |
| Code examples quality | PASS | curl examples show imports/headers, use realistic variable names ($MANDATE_RUNTIME_KEY), show auth pattern |
| Developer clarity | PASS | Structured for machine consumption. Note on line 8 directs humans to the main docs. |

## Findings

### medium: Missing "Next Steps" CardGroup at bottom

- **Line(s):** 276 (end of file)
- **Rule:** Page structure (every page must have "Next Steps" CardGroup)
- **Found:** Page ends with the "Raw Source" section and no CardGroup
- **Fix:** Add a Next Steps CardGroup at the bottom. Suggested cards: "Introduction" (/introduction) for human-friendly overview, "Handle Errors" (/guides/handle-errors) for error handling patterns, "Quickstart" (/quickstart) for getting started, "API Reference" (/api-reference/overview) for full endpoint docs.

### low: Claude Code install command may be outdated

- **Line(s):** 260
- **Rule:** Accuracy
- **Found:** `claude plugin:install claude-mandate-plugin`
- **Fix:** Verify this matches the current Claude Code plugin install flow. The quickstart page (line 38-39) uses a different command pattern: `/plugin marketplace add SwiftAdviser/claude-mandate-plugin` followed by `/plugin install mandate@mandate`. These two pages show different install methods. Ensure consistency or clarify that both are valid.

### low: OpenClaw install command differs from quickstart

- **Line(s):** 259
- **Rule:** Consistency
- **Found:** `openclaw plugins install @mandate.md/mandate-openclaw-plugin`
- **Fix:** The quickstart page (line 72) uses `openclaw plugin install @mandate.md/mandate-openclaw-plugin` (singular "plugin"). This page uses `openclaw plugins install` (plural "plugins"). Verify which is correct and align both pages.

## Developer Experience Notes

This page is designed for AI agent consumption, not human developers, and it excels at that purpose. Every section is self-contained, uses exact curl commands, and includes complete request/response examples. The "Mandatory Security Rules" on lines 23-32 are direct and unambiguous, which is critical for an AI agent that might otherwise skip validation. The fail-safe behavior on lines 36-42 gives exact retry logic. The block reason table on lines 164-179 and intent states table on lines 184-194 are comprehensive quick references. The tool-to-endpoint map on lines 226-238 is unique to this page and extremely useful for agents that need to translate between CLI commands and API calls. The main concern for a developer is that two install commands (Claude Code plugin, OpenClaw plugin) differ from the quickstart page, which could cause confusion if a developer cross-references both pages.

## Score

- Critical: 0, High: 0, Medium: 1, Low: 2
- **Overall:** WARN
