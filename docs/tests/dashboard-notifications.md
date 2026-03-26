# QA Report: dashboard/notifications.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 2 inline = 5) |
| 7 | Correct terminology | PASS |
| 8 | UI elements clearly described, step-by-step actions | PASS |

## Findings

### PASS: All structural checks pass
Clean frontmatter. No em dashes. No filler words. Terminology correct. 5 cross-links.

### GOOD: Step-by-step for each channel (lines 17-48)
Telegram (5 steps), Slack (3 steps), and custom webhook (3 steps) each have numbered procedures. This is exactly what dashboard docs need.

### GOOD: Triggering events table (lines 55-61)
Four events with descriptions and urgency signals ("most time-sensitive", "investigate promptly", "immediate attention required"). Helps users prioritize which events to enable.

### GOOD: Per-channel event configuration (line 62)
"Enable or disable each event type per channel" with a concrete example (all events to webhook, only critical to Telegram). Practical operational advice.

### GOOD: Test button section (lines 65-66)
Mentioning the test button with realistic data is helpful. The Warning callout for troubleshooting failed tests (lines 68-70) covers common failure modes per channel.

### MINOR: Discord section is placeholder (lines 38-39)
"Coming soon" with no timeline. Consider removing it entirely or adding an expected date. Placeholder sections reduce trust in documentation accuracy.

### MINOR: No mention of notification frequency or rate limiting
If an agent triggers 100 failed transactions in a minute, do I get 100 Telegram messages? Is there batching or throttling? This is critical for avoiding alert fatigue.

### MINOR: No mention of how to unlink/disconnect a channel
Steps for linking Telegram are clear, but how do I disconnect it? Remove Slack webhook? The page covers setup but not teardown.

## Developer Experience Notes

- The strongest aspect is the per-channel step-by-step setup. A developer can follow these instructions and have notifications working in minutes.
- Missing: notification message format. What does the Telegram message look like? What fields does the Slack card contain? Knowing the format helps users understand what they'll see.
- Missing: can I configure notification recipients per agent? Or are notifications account-wide? For teams managing multiple agents, per-agent routing matters.
- Missing: quiet hours / do-not-disturb. Can I mute notifications during maintenance windows?
- The custom webhook section correctly links to the Webhooks page for details. Good separation of concerns.
- The Tip about pinning the bot chat (line 25) is a small but genuinely useful UX suggestion.

## Score

**8.5/10** - Excellent setup guide with clear per-channel instructions. The Discord placeholder and missing disconnect/unlink guidance are the main weaknesses. Adding notification format examples and rate limiting info would make this page comprehensive.
