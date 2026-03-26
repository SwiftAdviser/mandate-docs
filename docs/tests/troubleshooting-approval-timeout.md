# QA Report: troubleshooting/approval-timeout.mdx

**Reviewed:** 2026-03-26
**Reviewer:** Claude Opus 4.6 (doc QA agent)

---

## Checklist

| # | Rule | Pass? | Notes |
|---|------|-------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS | All three present. |
| 2 | No em dashes (U+2014) | PASS | None found. |
| 3 | No filler words | PASS | None found. |
| 4 | Short paragraphs (2-4 sentences) | PASS | All within limit. |
| 5 | "Next Steps" CardGroup at bottom | PASS | Present, 3 cards. |
| 6 | 3-5 cross-links | PASS | 3 links: /guides/handle-approvals (line 84), /dashboard/notifications (line 87), /reference/intent-states (line 90). |
| 7 | Terminology | PASS | Uses "intent", "validate", "runtime key" correctly. |
| 8 | Troubleshooting: exact errors, step-by-step, cause-solution mapping | PASS | Clear cause-solution structure with code. |

---

## Findings

### Lines 8-11: Strong opening with concrete TTLs
Both TTLs (1-hour approval, 10-minute broadcast) stated in the first paragraph. The TTL reference table on lines 14-18 reinforces this. Excellent for quick scanning.

### Lines 14-18: TTL reference table
Clean, minimal table. States are in code format, TTLs are human-readable, consequences are specific. This table alone could answer most approval timeout questions.

### Lines 20-32: Three timeout causes
Each cause has a short heading and 1-2 sentence explanation. The "Agent not polling" cause (lines 31-32) is the most actionable for developers.

### Lines 36-61: Code example with nested try-catch
The code shows:
- `waitForApproval` with matching 1-hour timeout
- `onPoll` callback for status updates
- Expiry detection and re-validation

This is a complete, copy-paste-ready pattern. The nested try-catch may look complex, but it reflects the real control flow.

### Line 53: Error detection via string matching
`pollErr.message.includes('expired')` is brittle. If the SDK ever changes the message text, this breaks. Is there a typed error class or error code for expiry? If `ExpiredError` exists, the docs should use it. If not, this should be documented as the recommended detection pattern with a note about its fragility.

### Lines 63-71: Notification setup
Lists three channels (Telegram, Slack, Dashboard) with setup instructions. Practical and specific.

### Lines 73-79: Broadcast expiry recovery
Clear: "Start the entire flow over." No ambiguity. The Tip callout reinforces "broadcast immediately after approval."

### Lines 81-93: Next Steps has exactly 3 cards
At the minimum threshold. A card to /troubleshooting/common-errors (which has the 202 approval section) or /sdk/mandate-client (for the `waitForApproval` API reference) would add value.

### Missing: No mention of what the agent receives when approval is rejected
The page covers expiry but does not show the response when an owner actively rejects. The `status.status === 'rejected'` case is absent from the code example. An agent needs to handle both rejection and expiry.

### Missing: No mention of webhook-based approval notification
The code shows polling via `waitForApproval()`. Does Mandate support webhooks for approval decisions? If so, it should be mentioned as an alternative to polling.

---

## Developer Experience Notes

**Scenario: AI agent calls `waitForApproval()` and it times out.**

1. Agent sees timeout or expiry. Searches for "approval timeout" or "approval expired". Finds this page.
2. TTL table immediately answers "how long do I have?" (1 hour pending, 10 minutes post-approval).
3. Three causes section helps diagnose: is it the owner, the agent, or the TTL?
4. Code example shows the full recovery pattern: detect expiry, re-validate.
5. Notification setup section tells the owner how to avoid missing approvals.

**Verdict:** The page handles the happy path of expiry well. The gap is rejection handling: an agent needs to distinguish between "owner said no" and "owner did not respond." Adding the `status === 'rejected'` branch to the code example would complete the picture.

**Strength:** The TTL table is a standout feature. Developers will bookmark this for the numbers alone.

---

## Score

**8/10**

Clean structure, concrete TTLs, working code example. Deductions: string-based error detection is brittle (-0.5), no rejection handling shown (-0.5), no webhook mention (-0.5), Next Steps at minimum (-0.5).
