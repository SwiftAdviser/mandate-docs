# Documentation QA Summary Report

**Date:** 2026-03-26
**Pages tested:** 88 (across 11 sections)
**Sub-agents used:** 11 (one per section)
**Perspective:** Developer building an AI agent with a wallet (using nanoclaw/ClawRouter as reference)

---

## Overall Results

| Section | Pages | PASS | WARN | FAIL | Critical | High | Medium | Low |
|---------|-------|------|------|------|----------|------|--------|-----|
| Top-level | 5 | 1 | 4 | 0 | 0 | 1 | 3 | 8 |
| Concepts | 7 | 0 | 6 | 1 | 1 | 4 | 5 | 12 |
| Guides | 10 | 2 | 8 | 0 | 0 | 0 | 13 | 19 |
| Security | 7 | 0 | 6 | 1 | 0 | 1 | 16 | 7 |
| Troubleshooting | 5 | 0 | 5 | 0 | 0 | 0 | 5 | 8 |
| SDK | 7 | 0 | 7 | 0 | 0 | 0 | 8 | 10 |
| CLI | 12 | 0 | 12 | 0 | 0 | 0 | 12 | 14 |
| Integrations | 10 | 2 | 8 | 0 | 0 | 0 | 10 | 12 |
| Dashboard | 10 | 0 | 10 | 0 | 0 | 2 | 10 | 8 |
| Reference + API | 8 | 5 | 3 | 0 | 0 | 0 | 3 | 5 |
| Snippets | 7 | 5 | 2 | 0 | 0 | 0 | 2 | 2 |
| **TOTAL** | **88** | **15** | **71** | **2** | **1** | **8** | **87** | **105** |

**Overall health: 83/100** (good baseline, no critical structural issues)

---

## FAIL Pages (must fix)

### 1. concepts/glossary.mdx
- **Critical:** Missing Next Steps CardGroup entirely (required on every page)
- **High:** Uses "transaction request" instead of "intent" (line 71)

### 2. security/envelope-verification.mdx
- **High:** Zero code examples for the most implementation-heavy security flow (rawValidate + postEvent). A developer cannot implement envelope verification from this page alone.

---

## High Severity Findings (8 total)

| # | Page | Finding |
|---|------|---------|
| 1 | quickstart.mdx | Two em dashes (U+2014) in code comments, lines 136 and 206 |
| 2 | concepts/glossary.mdx | "transaction request" terminology, line 71 |
| 3 | concepts/intent-lifecycle.mdx | "transaction request" in description, line 9 |
| 4 | concepts/non-custodial.mdx | 2 high findings (see report for details) |
| 5 | concepts/intent-hash.mdx | Opening paragraph exceeds 60-word limit (71 words) |
| 6 | security/envelope-verification.mdx | No code examples for rawValidate + postEvent flow |
| 7 | dashboard/overview.mdx | Banned term "transaction requests" on line 25 |
| 8 | dashboard/approvals.mdx | Banned term "transaction request" on line 63 |

---

## Top 10 Recurring Patterns

These patterns appear across multiple sections. Fixing them systematically would have the highest impact.

### 1. Missing "## Next Steps" heading above CardGroups
**Affected:** 10+ pages across concepts, SDK, security sections
**Fix:** Add `## Next Steps` H2 heading before every closing CardGroup

### 2. Insufficient cross-links (fewer than 3)
**Affected:** cli/activate, cli/whoami, cli/event, reference/chain-reference, reference/error-codes, reference/rate-limits, dashboard/overview, dashboard/webhooks, sdk/constants
**Fix:** Add 1-2 more cross-links to each, targeting related pages

### 3. "transaction request" instead of "intent"
**Affected:** concepts/glossary, concepts/intent-lifecycle, dashboard/overview, dashboard/approvals
**Fix:** Find-and-replace "transaction request(s)" with "intent(s)"

### 4. Missing error output in code examples
**Affected:** Most CLI command pages, guides/register-agent, guides/x402-payments, security/envelope-verification
**Fix:** Add error/failure response examples alongside success examples

### 5. CodeGroup tab ordering
**Affected:** guides/register-agent, guides/validate-transactions, guides/handle-approvals
**Fix:** Reorder to: TypeScript SDK, Python, CLI, curl

### 6. Opening paragraphs exceed 60-word limit
**Affected:** concepts/policy-engine (67 words), concepts/reason-field (62 words), concepts/intent-hash (71 words)
**Fix:** Trim to under 60 words

### 7. CLI page title inconsistency
**Affected:** cli/event, cli/status, cli/approve, cli/scan use bare names while cli/login, cli/validate, cli/transfer use "mandate X"
**Fix:** Standardize all CLI page titles to "mandate {command}" pattern

### 8. Missing code examples in security docs
**Affected:** 5 of 7 security pages have zero code
**Fix:** Add SDK examples for circuit breaker check, risk scanning, credential rotation

### 9. No testing/sandbox guidance in security section
**Affected:** All 7 security pages
**Fix:** Add "How to test" section or callout per page

### 10. Block reason code inconsistency
**Affected:** guides/write-mandate-md uses `spend_limit_exceeded`, guides/handle-errors uses `per_tx_limit_exceeded`
**Fix:** Align to the canonical values in reference/block-reasons.mdx

---

## Developer Experience Assessment

Testing from the perspective of a developer building an AI agent with a wallet (nanoclaw-style):

### What works well
- **Quickstart is strong.** Four clear paths (Claude Code, OpenClaw, SDK, CLI). A developer knows where to start.
- **handle-errors.mdx is the gold standard.** Complete error taxonomy, code examples, both success and failure paths.
- **Reference tables are excellent.** block-reasons, intent-states, policy-fields are all scannable and complete.
- **Writing quality is consistently high.** Zero em dashes in 86 of 88 pages. Zero filler words everywhere. Terminology is 95%+ correct.
- **intent-states.mdx is the best page.** Mermaid diagram + tables + transitions + quota behavior.

### What needs work
- **Vercel AI integration is the weakest page (5.5/10).** Missing install command, no env var table, unused import. A developer using Vercel AI SDK cannot follow this page.
- **GOAT SDK and AgentKit examples stop before agent wiring.** Not copy-paste ready.
- **Circuit breaker troubleshooting is written for humans, not AI agents.** An agent receiving a 403 has no code to copy.
- **Security docs lack implementation examples.** For a product whose value proposition is security, 5/7 pages having zero code is a gap.
- **No testing/sandbox guidance anywhere.** How to trigger a circuit breaker in test? How to verify reason scanning catches edge cases? Missing entirely.
- **sdk/errors.mdx has a copy-paste bug:** 3 examples omit the required `reason` parameter. A developer copying these will get runtime errors.

### nanoclaw/ClawRouter-specific gaps
- No integration guide for nanoclaw (lightweight agent framework)
- ClawRouter model routing not mentioned in any integration page
- The integrations overview matrix should include nanoclaw as a supported framework

---

## Section Scores

| Section | Score | Notes |
|---------|-------|-------|
| Reference + API | 9.0/10 | Cleanest section. Tables are excellent. |
| Snippets | 9.0/10 | Self-contained, consistent. Two minor type alignment issues. |
| Top-level | 8.5/10 | Introduction and quickstart are strong entry points. |
| Guides | 8.0/10 | handle-errors and codebase-scanner are gold standard. Others need error paths. |
| SDK | 8.0/10 | mandate-client is excellent. mandate-wallet and errors need work. |
| Troubleshooting | 8.0/10 | intent-hash-mismatch is best. circuit-breaker needs agent perspective. |
| Integrations | 7.5/10 | Vercel AI drags average down. Claude Code and OpenClaw are solid. |
| Dashboard | 7.5/10 | Terminology violations. No screenshots in any page. |
| CLI | 7.5/10 | Inconsistent titles. Missing error output across most pages. |
| Concepts | 7.0/10 | Glossary is the only FAIL. Opening paragraphs need trimming. |
| Security | 7.0/10 | Biggest gap: no code in most pages. Envelope verification is FAIL. |

---

## Priority Fix List

### P0: Fix now (breaks trust or misleads)
1. `sdk/errors.mdx`: Add `reason` parameter to 3 transfer examples (copy-paste bug)
2. `concepts/glossary.mdx`: Add Next Steps CardGroup
3. `security/envelope-verification.mdx`: Add rawValidate + postEvent code example
4. `quickstart.mdx`: Replace 2 em dashes in code comments

### P1: Fix this week (terminology and structure)
5. Replace "transaction request(s)" with "intent(s)" in 4 pages
6. Add missing cross-links to 9 pages below the 3-link minimum
7. Add "## Next Steps" heading above CardGroups in 10+ pages
8. Standardize CLI page titles to "mandate {command}" pattern
9. Fix CodeGroup tab ordering in 3 guide pages

### P2: Fix this sprint (developer experience)
10. Rewrite `integrations/vercel-ai.mdx` (missing install, env vars, unused import)
11. Complete `sdk/mandate-wallet.mdx` method documentation (param tables, return types)
12. Add code examples to 5 security pages
13. Add error output examples to CLI command pages
14. Complete GOAT SDK and AgentKit examples with full agent wiring

### P3: Backlog (nice to have)
15. Add testing/sandbox guidance to security section
16. Add monitoring/alerting guidance for circuit breaker, risk scanning
17. Add nanoclaw integration page
18. Add screenshots to dashboard pages
19. Align block reason codes between write-mandate-md and handle-errors
20. Trim 3 concept page opening paragraphs to under 60 words

---

## Files

All 88 individual page reports are in `/docs/tests/`:
- Testing methodology: `TESTING-GUIDE.md`
- This summary: `SUMMARY.md`
- Per-page reports: `{section}-{page-name}.md`
