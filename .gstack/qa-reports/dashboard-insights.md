# QA Report: dashboard/insights.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline = 4) |
| 7 | Correct terminology | PASS |
| 8 | UI elements clearly described, step-by-step actions | PASS |

## Findings

### PASS: All structural checks pass
Clean frontmatter. No em dashes. No filler words. Correct terminology. 4 cross-links.

### GOOD: Confidence levels table (lines 22-29)
Excellent breakdown with score ranges, labels, and actionable meaning. "Act on these first" and "Monitor before acting" give clear triage guidance.

### GOOD: Example insights (lines 61-63)
Three concrete examples with insight type and confidence score in parentheses. Developers can see exactly what to expect.

### GOOD: Insight card anatomy (lines 35-41)
Clear enumeration of card components. The evidence count detail ("Based on 47 transactions") is a nice specificity touch.

### MINOR: Accept action note about "new policy version" (line 49-52)
The Note callout is important but could be a Warning. Accepting an insight modifies live policy. The stakes are higher than "supplementary information."

### MINOR: 5-bar visual indicator (line 31)
Line 31: "A score of 0.85 fills approximately 4.25 bars" is oddly specific. The fractional bar fill is an unusual UI detail that may confuse rather than clarify. Consider simplifying to "approximately 4 out of 5 bars."

### MINOR: No mention of how frequently insights are generated
How often does Mandate analyze patterns? Real-time? Daily batch? After N transactions? This affects expectations.

### NOTE: Dismiss behavior (line 57)
"Dismissed insights do not reappear for the same pattern" is useful. The follow-up sentence about new insights for changed patterns is also helpful.

## Developer Experience Notes

- The page explains a feature that could be confusing (AI-generated recommendations) in concrete, actionable terms. The confidence scoring system gives users a framework for prioritization.
- Missing: can I see dismissed insights again? Is there an archive? If I dismissed something by mistake, can I undo?
- Missing: do insights trigger notifications? If a STRONG RECOMMENDATION appears, do I get a Telegram/Slack alert? Or must I check the dashboard?
- Missing: how much transaction history is needed before insights start appearing? A new agent with 5 transactions won't have meaningful patterns. Setting expectations here would prevent confusion.
- Missing: can I disable insights entirely? Some operators may prefer fully manual policy management.
- The "one click" accept flow is powerful but risky. Consider mentioning whether there's a preview/confirmation step before the policy change applies.

## Score

**8.5/10** - Well-structured page that makes an AI feature tangible and actionable. The confidence framework and examples are strong. Missing generation frequency and minimum data requirements are the main gaps. The accept action could use a stronger callout about its policy-modifying effect.
