# QA Report: troubleshooting/circuit-breaker-tripped.mdx

**Reviewed:** 2026-03-26
**Reviewer:** Claude Opus 4.6 (doc QA agent)

---

## Checklist

| # | Rule | Pass? | Notes |
|---|------|-------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS | All three present. Description is action-oriented. |
| 2 | No em dashes (U+2014) | PASS | None found. |
| 3 | No filler words | PASS | None found. |
| 4 | Short paragraphs (2-4 sentences) | PASS | All paragraphs within limit. |
| 5 | "Next Steps" CardGroup at bottom | PASS | Present, 3 cards. |
| 6 | 3-5 cross-links | PASS | 3 links: /security/circuit-breaker (line 78), /security/envelope-verification (line 81), /dashboard/circuit-breaker (line 84). |
| 7 | Terminology | PASS | Uses "circuit breaker" consistently. Does not use "kill switch" or "emergency stop" outside of the allowed context. |
| 8 | Troubleshooting: exact errors, step-by-step, cause-solution mapping | PASS | 4-step flow: determine type, investigate, reset, prevent. |

---

## Findings

### Line 9: Strong definition-first opening
First sentence names the HTTP status (403), the blockReason code, and the behavioral consequence (all transactions blocked). Excellent for programmatic consumers.

### Lines 11-26: Two trip types clearly distinguished
Manual vs. auto-trip is the key branch. Each has specific audit log events to search for (`circuit_breaker_activated` vs `circuit_breaker_auto_tripped`). This is directly actionable.

### Lines 23-26: Audit log event metadata described
Lists the exact fields in the event metadata (validated parameters, on-chain parameters, which fields differ). A developer knows exactly what to look for.

### Lines 36-44: Root cause analysis is thorough
Four causes listed: nonce collision, gas repricing, middleware modification, malicious behavior. Each has a brief explanation of the mechanism. This is the right level of detail.

### Line 46-48: Warning callout for malicious case
Correctly warns not to reset if malicious. Good security posture in docs.

### Lines 59-66: API reset via curl
Provides the curl command for programmatic reset. Uses `{agentId}` placeholder and `<sanctum-token>` placeholder. Both are clear.

### Line 63: "sanctum-token" is not standard terminology
The writing guide defines "runtime key" as the correct term for agent auth. But `<sanctum-token>` appears to be a different auth mechanism (owner-level, not agent-level). This is not a terminology violation, but the term "sanctum" is unexplained. A brief note like "(your owner authentication token from the dashboard)" would help.

### Lines 70-73: Prevention checklist
Bullet-point prevention steps are actionable. Recommends `MandateWallet` class as the primary solution.

### Lines 75-87: Next Steps has exactly 3 cards
At the minimum threshold. All three link to security/dashboard pages. Missing a link to a related troubleshooting page (e.g., /troubleshooting/common-errors for the 403 circuit breaker entry) or to /sdk/mandate-wallet (since step 4 recommends it).

### Missing: No code example for detecting the circuit breaker error
The common-errors.mdx page shows the `CircuitBreakerError` catch pattern, but this dedicated page does not include SDK error detection code. A developer landing here directly (not via common-errors) has no code to copy.

### Missing: No mention of how to check circuit breaker status programmatically
Step 1 says "Open the dashboard." There is no API call shown for checking circuit breaker status before attempting validation. An agent that wants to check proactively has no guidance.

---

## Developer Experience Notes

**Scenario: AI agent gets a 403 with `blockReason: "circuit_breaker_active"`.**

1. Agent searches for "circuit_breaker_active" or "circuit breaker tripped". Finds this page.
2. The opening immediately confirms what the error means: all transactions blocked, human must reset.
3. Agent reads step 1: two possible trip types. Agent cannot check the audit log itself (that requires dashboard/owner access). The agent's only action is to report the error and stop.
4. Steps 2-3 are for the owner, not the agent. This is appropriate, but the page does not explicitly say "if you are the agent, stop here and notify the owner."
5. Step 4 prevention is useful for the developer writing the agent code.

**Verdict:** The page is excellent for human operators investigating a circuit breaker trip. For an AI agent that just received a 403, the page is less immediately useful because the agent cannot perform steps 1-3. Adding a "If you are the agent" callout at the top that says "stop all transactions, notify the owner, do not retry" would make this page work for both audiences.

---

## Score

**7.5/10**

Well-structured investigation flow for human operators. Good cause analysis and prevention steps. Deductions: no SDK error detection code on the page (-0.5), "sanctum-token" unexplained (-0.5), no programmatic status check (-0.5), no agent-perspective callout (-0.5), Next Steps at minimum (-0.5).
