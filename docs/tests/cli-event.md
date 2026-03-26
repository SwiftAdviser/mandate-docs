# QA Report: cli/event.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PARTIAL |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | FAIL (only 2 cards, no inline links) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 2 (frontmatter title)**: Title is "Event", not "mandate event". Every other CLI page uses the pattern "mandate <command>" (e.g., "mandate login", "mandate validate"). Inconsistent.
- **Line 6 (cross-links)**: Only 2 cards. Needs at least 1 more. Suggested: `/cli/validate` (the command that precedes event), `/guides/handle-errors` (what happens on envelope mismatch), or `/concepts/intent-hash` (the hash being verified).
- **Line 9**: Opening paragraph explains what `event` does, why, and what happens on match/mismatch. Self-contained. Good for LLM citation.
- **Line 11**: "This command is required after every `validate --raw` or `transfer --raw` flow." Clear prerequisite.
- **Line 19-23**: Arguments and Options tables are clean and consistent with sibling pages.
- **Line 44-51**: "When to use this" section with numbered flow is excellent. Shows exactly where `event` fits in the lifecycle.
- **Line 52**: "For preflight validation (the default, without --raw), you do not need event." Important disambiguation.
- **Line 54-56**: Warning about circuit breaker is critical. Well placed.

## Developer Experience Notes

- **Lifecycle context is strong**: The numbered flow (lines 46-51) makes it obvious when to use `event`. No ambiguity.
- **Circuit breaker warning**: A developer who misuses this command understands the consequences. Good.
- **Missing**: No error output example. What if I post a wrong txHash? What if the intentId is invalid or already confirmed? The warning says the circuit breaker trips, but no example of that error response.
- **Frontmatter inconsistency**: Title "Event" breaks the pattern. Should be "mandate event".

## Score

**7/10**

Good content, but below cross-link minimum, inconsistent title, and no error output. The lifecycle context and circuit breaker warning are standout sections.
