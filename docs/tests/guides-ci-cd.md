# Test Report: CI/CD Integration

**File:** guides/ci-cd.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "CI/CD Integration" |
| Frontmatter: sidebarTitle | PASS | "CI/CD" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 3 cards |
| Cross-links (3-5) | WARN | count: 3 (inline: /guides/validate-transactions; cards: /guides/codebase-scanner, /cli/scan, /guides/validate-transactions) |
| Correct terminology | WARN | See findings below |
| Code examples quality | PASS | YAML and bash examples are realistic and copy-pasteable |
| Steps are followable | PASS | Clear per-platform instructions |
| Error handling shown | PASS | Exit codes and error output explained |
| Developer clarity | PASS | Practical CI recipes |

## Findings

### Medium: Cross-links below minimum

- **Line(s):** 107-119
- **Rule:** 3-5 cross-links to related pages
- **Found:** Only 3 cards in Next Steps, and only 1 inline link (/guides/validate-transactions). Total unique cross-links: 3, at the minimum.
- **Fix:** Add a 4th card to /guides/fail-safe or /sdk/overview. Add inline links in the "How do you fix findings?" section to /guides/handle-errors or /sdk/mandate-client.

### Low: Terminology - "preflight" in detection patterns

- **Line(s):** 82
- **Rule:** Use "validate" not "preflight" (unless explaining the alias)
- **Found:** `mandate.validate`, or `mandate.preflight`
- **Fix:** This describes what the scanner detects (it recognizes both terms as protection signals). Acceptable in this context, but could add a parenthetical: "(`mandate.preflight` is a legacy alias for `mandate.validate`)".

### Low: Content duplication with codebase-scanner.mdx

- **Line(s):** 68-82
- **Rule:** DRY, consider shared snippets
- **Found:** The "What does the scanner check?" table is nearly identical to the pattern list in guides/codebase-scanner.mdx.
- **Fix:** Consider importing a shared snippet for the scanner patterns, or reference the codebase scanner guide instead of repeating the table.

### Low: Missing error handling in "fix findings" code example

- **Line(s):** 88-99
- **Rule:** Show both success and error paths
- **Found:** The "After: protected" code shows `validate()` then `sendTransaction()` but no try/catch around either call.
- **Fix:** Add minimal error handling to the fix example, or reference the handle-errors guide explicitly.

## Developer Experience Notes

The guide is practical and ready to copy-paste into CI pipelines. GitHub Actions and GitLab CI examples are both covered, which is good. The pre-commit hook section gives developers local protection. The "fix findings" section bridges the gap between detection and resolution. As a developer setting up CI, I can follow this in under 5 minutes. The main improvement would be a complete "before and after" example showing an unprotected file, the scanner output, and the fixed file.

## Score
- Critical: 0, High: 0, Medium: 1, Low: 3
- **Overall:** WARN
