# QA Report: dashboard/approvals.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 2 inline = 5) |
| 7 | Correct terminology | FAIL |
| 8 | UI elements clearly described, step-by-step actions | PASS |

## Findings

### FAIL: Banned term "transaction request" (line 63)
Line 63: "The agent must submit a new transaction request." The terminology table specifies "intent" instead of "transaction request". This should read "The agent must submit a new intent."

### GOOD: Card fields table (lines 17-26)
Excellent enumeration of approval card fields. The pulse indicator and hover behavior for addresses are dashboard-specific details that help users recognize what they're looking at.

### GOOD: Risk level badges table (lines 30-36)
Clear, actionable descriptions. "Investigate before approving" for CRITICAL is the right tone.

### GOOD: Approve/reject section (lines 39-49)
Clean description of the two actions with the optional notes feature. The Tip callout about adding notes to rejections is practical advice.

### MINOR: No mention of approval queue ordering
When I have 15 pending approvals, what order are they shown in? Newest first? Highest risk first? Expiring soonest? This matters for triage.

### MINOR: No mention of filtering or search
If I manage multiple agents, can I filter approvals by agent? By risk level? The page describes a flat paginated list without any filtering capability.

### MINOR: Expiration section (lines 62-63) lacks specifics
"Approval requests have a time limit" but the actual duration is never stated. Is it 1 hour? 24 hours? Configurable? This is critical operational information.

## Developer Experience Notes

- The page covers the core approval workflow well: see pending items, review details, approve or reject.
- The notification channel summary (lines 53-59) is a useful cross-reference, but it's essentially duplicating the Notifications page. Consider trimming to one sentence with a link.
- Missing: can I approve/reject from Telegram or Slack directly? Or must I use the dashboard? This is a common question for on-call operators.
- Missing: multi-approval scenarios. If a policy requires 2 approvers, how does that work? Or is it always single-approver?
- Missing: what happens if I approve a transaction and the circuit breaker trips between approval and execution? Edge case, but important for operators.
- The "Time remaining" field in the card table mentions a countdown but no default duration or configuration method.

## Score

**7.5/10** - Good coverage of the approval workflow with one terminology violation. The missing expiration duration is a significant gap for operators. Fixing the terminology, adding expiration specifics, and mentioning queue ordering would bring it to 9+.
