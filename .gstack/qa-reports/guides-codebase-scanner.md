# Test Report: Codebase Scanner

**File:** guides/codebase-scanner.mdx
**Date:** 2026-03-26
**Status:** PASS

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Codebase Scanner" |
| Frontmatter: sidebarTitle | PASS | "Codebase Scanner" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 4 cards |
| Cross-links (3-5) | PASS | count: 4 (inline: /integrations/claude-code, /integrations/openclaw; cards: /cli/scan, /guides/ci-cd, /integrations/claude-code, /guides/validate-transactions) |
| Correct terminology | PASS | Uses correct terminology throughout |
| Code examples quality | PASS | CLI commands with flags shown, output examples included |
| Steps are followable | PASS | Clear: run scan, read output, fix findings |
| Error handling shown | N/A | CLI tool, exit codes serve as error handling |
| Developer clarity | PASS | Practical with real output examples |

## Findings

### Low: No mention of Python file scanning

- **Line(s):** 41
- **Rule:** Developer clarity
- **Found:** `The scanner checks .ts, .js, .tsx, and .jsx files.`
- **Fix:** If Python agents are a target audience (Python examples appear in other guides), note that Python files are not currently scanned, or that Python support is planned.

### Low: CI section duplicates content from ci-cd.mdx

- **Line(s):** 63-99
- **Rule:** DRY principle
- **Found:** The GitHub Actions YAML and pre-commit hook are nearly identical to what appears in guides/ci-cd.mdx.
- **Fix:** Consider importing a shared snippet, or referencing the CI/CD guide instead of duplicating the examples. Alternatively, keep a brief example here and link to the full CI/CD guide for advanced setups.

## Developer Experience Notes

The guide is straightforward and practical. As a developer, I can run `npx @mandate.md/cli scan` immediately and understand the output. The exit code explanation (0 = clean, 1 = findings) makes CI integration obvious. The JSON output option is useful for custom tooling. The auto-scan in plugins section is a nice touch. The detection patterns list gives me confidence the scanner will find real issues in my codebase.

## Score
- Critical: 0, High: 0, Medium: 0, Low: 2
- **Overall:** PASS
