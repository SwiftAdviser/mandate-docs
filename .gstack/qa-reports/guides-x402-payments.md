# Test Report: x402 Payment Protocol

**File:** guides/x402-payments.mdx
**Date:** 2026-03-26
**Status:** WARN

## Checklist

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS | "x402 Payment Protocol" |
| Frontmatter: sidebarTitle | PASS | "x402 Payments" |
| Frontmatter: description | PASS | Action-oriented, includes keywords |
| No em dashes | PASS | None found |
| No filler words | PASS | None found |
| Short paragraphs | PASS | All paragraphs within 2-4 sentences |
| Next Steps CardGroup | PASS | Present at bottom with 4 cards |
| Cross-links (3-5) | PASS | count: 4 (cards: /sdk/mandate-wallet, /guides/validate-transactions, /reference/chain-reference, /guides/handle-errors) |
| Correct terminology | WARN | See findings below |
| Code examples quality | WARN | See findings below |
| Steps are followable | PASS | 5-step flow is clear, both auto and manual paths shown |
| Error handling shown | WARN | See findings below |
| Developer clarity | WARN | See DX notes |

## Findings

### Medium: Terminology - "API keys" used in description of x402 concept

- **Line(s):** 9
- **Rule:** Use "runtime key" not "API key"
- **Found:** `No API keys, no subscriptions: the agent pays per-request.`
- **Fix:** This refers to external API keys (not Mandate's runtime key), so the meaning is different. However, it could confuse readers scanning for terminology. Consider: "No authentication tokens, no subscriptions: the agent pays per-request."

### Medium: No error handling shown for x402Pay() or manual flow

- **Line(s):** 40-56, 70-116
- **Rule:** Show both success and error paths
- **Found:** Neither the `x402Pay()` example nor the manual flow examples include try/catch. What happens if the payment is blocked by policy? What if the 402 header is malformed? What if the retry fails?
- **Fix:** Add try/catch around `x402Pay()` showing PolicyBlockedError handling. For the manual flow, add error checks after each step (parse failure, transfer blocked, retry failure).

### Medium: Manual flow code is TypeScript-only, no CodeGroup

- **Line(s):** 70-116
- **Rule:** Use code tabs: TypeScript SDK, Python, CLI, curl
- **Found:** Steps 1-4 of the manual flow are all bare TypeScript code blocks, not wrapped in a CodeGroup. No Python, CLI, or curl equivalents.
- **Fix:** Either wrap in a CodeGroup with at least Python and curl tabs, or add a note that the manual flow is TypeScript SDK-only.

### Low: Missing prerequisite - wallet setup

- **Line(s):** (missing)
- **Rule:** Guides should mention prerequisites
- **Found:** The guide jumps straight into x402Pay() without mentioning that you need a funded MandateWallet with a private key and runtime key.
- **Fix:** Add a prerequisites note linking to register-agent and MandateWallet setup.

## Developer Experience Notes

The x402 concept is well explained with the ASCII flow diagram. The one-liner `x402Pay()` is appealing for the happy path. The policy considerations section is practical and warns about real pitfalls (malicious servers inflating amounts). However, as a developer, I would struggle with the error path. What does my agent do if a critical API call returns 402, the payment is blocked by policy, and the agent can not proceed? The manual flow steps are clear but lack error handling at each stage. The guide would benefit from a complete end-to-end example with error handling included.

## Score
- Critical: 0, High: 0, Medium: 3, Low: 1
- **Overall:** WARN
