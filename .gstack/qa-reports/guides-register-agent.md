# Test Report: Register an Agent

**File:** guides/register-agent.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "Register an Agent" |
| Frontmatter: sidebarTitle | PASS | "Register Agent" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 4 cards |
| Cross-links (3-5) | PASS | count: 7 (inline: /dashboard/agents x2, /dashboard/policy-builder; cards: 4) |
| Correct terminology | PASS | Uses "runtime key", "dashboard", "policy engine" correctly |
| Code examples quality | WARN | See findings below |
| Steps are followable | WARN | See findings below |
| Error handling shown | WARN | Registration error handling not shown |
| Developer clarity | WARN | See DX notes |

## Findings

### Medium: CodeGroup tab order wrong - Python before CLI

- **Line(s):** 38-64
- **Rule:** CodeGroup tab order: TypeScript SDK, Python, CLI, curl
- **Found:** Order is TypeScript, CLI, Python, curl
- **Fix:** Swap the CLI and Python tabs so order is: TypeScript, Python, CLI, curl

### Medium: No error handling shown for registration call

- **Line(s):** 22-79
- **Rule:** Code examples must show both success and error paths
- **Found:** All four code examples show only the success path. No try/catch, no HTTP status check for Python/curl.
- **Fix:** Add a try/catch around the TypeScript `register()` call showing what happens on failure (e.g., duplicate agent name, invalid address). Add status code check for Python and curl examples.

### Low: Python example missing error handling

- **Line(s):** 48-64
- **Rule:** Show both success and error paths
- **Found:** `resp.json()` called without checking `resp.status_code`
- **Fix:** Add `resp.raise_for_status()` or a status code check before accessing the response body.

### Low: No prerequisites section

- **Line(s):** (missing)
- **Rule:** Guides should mention prerequisites
- **Found:** No mention of Node.js version requirement, no mention of whether you need a wallet address first.
- **Fix:** Add a brief prerequisites note: Node.js 18+, an EVM wallet address, and optionally a target chain decision.

## Developer Experience Notes

The guide is followable as a first step. The registration flow is clear: call register, get credentials, store them, share claim URL. However, as a developer building an AI agent, I would want to know: (1) what happens if registration fails (network error, duplicate name), (2) whether I need to have a funded wallet already, (3) what chains are supported beyond Base Sepolia. The claim flow explanation is well done. The default policy table is helpful. The credential storage section is practical with real commands.

## Score
- Critical: 0, High: 0, Medium: 2, Low: 2
- **Overall:** WARN
