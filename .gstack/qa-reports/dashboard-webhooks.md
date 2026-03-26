# QA Report: dashboard/webhooks.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | FAIL |
| 7 | Correct terminology | PASS |
| 8 | UI elements clearly described, step-by-step actions | WARN |

## Findings

### FAIL: Only 2 cross-links in Next Steps (lines 107-113)
Two cards: Notifications and API Reference. Plus 1 inline link (Notifications page, line 31). Total: 3, which is at the minimum threshold. However, the Next Steps section itself has only 2 cards. Adding a third card (e.g., Handle Errors guide, or Security overview) would strengthen this.

### GOOD: Payload format with JSON example (lines 37-52)
Realistic JSON payload with all relevant fields. Uses correct example values (`ag_abc123`, `int_xyz789`, `0xRecipientAddress`). The timestamp even uses today's date format.

### GOOD: Secret verification with TypeScript code (lines 62-74)
Working code example for HMAC-SHA256 verification. Includes the import, function, and usage in a handler. This is directly copy-pasteable.

### GOOD: Retry policy table (lines 83-89)
Clear escalating delays (1 min, 5 min, 30 min) with 3 attempts total. Developers know exactly what to expect.

### GOOD: Warning callout for signature verification (lines 76-78)
Correctly flags the security implication of not verifying signatures.

### WARN: Dashboard UI elements not described
This page is heavily API-focused. It mentions "the dashboard" for the webhook delivery log (line 90) but doesn't describe where to find it in the UI, what it looks like, or how to navigate to it. The page title places it in the dashboard section but the content reads more like an API reference.

### MINOR: No error payload example
The payload format section shows a successful event. What does an `intent_failed` payload look like? Does `metadata` include the `blockReason`? Developers building webhook handlers need to know the shape of all event types.

### MINOR: No mention of webhook timeout
"If your endpoint... times out" (line 82) but no timeout duration specified. Is it 5 seconds? 30 seconds? Developers need this to size their handler appropriately.

### MINOR: Code example only in TypeScript (lines 62-74)
The writing guide specifies code tabs in order: TypeScript, Python, CLI, curl. The verification example only shows TypeScript. A Python equivalent would help teams not using Node.

## Developer Experience Notes

- This page serves a dual purpose: dashboard configuration and API/integration reference. It does the API side well but the dashboard side poorly.
- The webhook API table (lines 15-19) is helpful for programmatic management. GET, PUT, and POST test are the essential operations.
- Missing: webhook delivery log. Line 90 mentions it but doesn't describe it. Where is it? What does it show? Can I retry failed deliveries from the UI?
- Missing: IP allowlisting. Can I restrict which IPs Mandate sends webhooks from? Enterprise users often need to allowlist webhook source IPs.
- Missing: webhook deactivation. How do I disable a webhook without deleting the configuration?
- The test endpoint (lines 94-101) is well-documented with a curl example. Good.
- Missing: rate limits on webhook deliveries. If an agent processes 1000 transactions, are all 1000 delivered as individual webhooks?

## Score

**7.5/10** - Strong API-side documentation with good code examples and security guidance. Falls short on dashboard UI description and the minimum cross-link requirement in Next Steps. Adding a webhook delivery log section, error payload examples, and a third Next Steps card would bring it to compliance.
