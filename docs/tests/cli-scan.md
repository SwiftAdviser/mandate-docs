# QA Report: cli/scan.mdx

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

- **Line 2 (frontmatter title)**: Title is "Scan", not "mandate scan". Same pattern break as event, status, approve.
- **Line 4**: Description: "Zero config, zero auth, CI-friendly." Punchy and accurate.
- **Line 9**: Opening paragraph lists the specific patterns detected (`.sendTransaction()`, `.transfer()`, `writeContract()`, "and 7 other patterns") and the matching criteria (no corresponding Mandate validation in the same file). Excellent density.
- **Line 27-34**: Options table includes `--json`, `--verbose`, `--ignore`, and `--no-telemetry`. Complete.
- **Line 38-52**: Patterns table lists all 10 patterns with examples. A developer can verify their code against this list.
- **Line 53**: Protection detection logic is explained: imports from `@mandate`, `MandateClient`, `MandateWallet`, etc. Also checks `package.json` and `MANDATE.md`. Thorough.
- **Line 56-61**: Exit codes table. Critical for CI integration. Clean.
- **Line 64-78**: Human-readable output example is realistic. Shows file paths, line numbers, pattern matches, and the "UNPROTECTED" marker.
- **Line 82-101**: JSON output example. Complete with `filesScanned`, `findings` array, and `summary` object.
- **Line 103-128**: CI integration section covers GitHub Actions, pre-commit hooks, and GitLab CI. Three examples.
- **Line 132-134**: Tip about running scan early in the pipeline. Practical.

## Developer Experience Notes

- **Best standalone page in the set**: A developer can go from "what is this" to "running in CI" without leaving the page.
- **Patterns table (lines 38-52)**: I can audit my codebase against this list before even running the command. Saves a round trip.
- **CI examples (lines 103-128)**: Three CI platforms covered with copy-paste configs. GitHub Actions, pre-commit, GitLab. Missing: Bitbucket Pipelines, but three is enough.
- **Exit codes**: Critical for CI. A developer writing `|| exit 1` in a pre-commit hook needs to know exit code 1 means findings.
- **No issues found**: This page is the most complete in the CLI set.

## Score

**9/10**

Excellent page. Only deduction: frontmatter title pattern ("Scan" vs "mandate scan"). Content, examples, and CI integration are all strong.
