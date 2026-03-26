# QA Report: integrations/claude-code.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (4 cards) |
| 7 | Terminology compliance | PASS |
| 8 | Install command shown | PASS (lines 20-21) |
| 9 | Configuration steps clear | PASS |
| 10 | Code example complete | PASS (example flow lines 104-131) |
| 11 | Tools/actions table present | PARTIAL -- no formal table; gate triggers are described in prose and lists |

## Findings

- **Line 11**: "PostToolUse records validation tokens when the agent validates with Mandate, and PreToolUse blocks transaction commands that lack a valid token." This sentence is technically accurate but the hook execution order (PostToolUse before PreToolUse) can confuse readers who expect chronological ordering. The "How the two-phase gate works" section (line 27) clarifies this well.
- **Lines 20-21**: Install uses `/plugin marketplace add` and `/plugin install`. These are slash commands typed inside Claude Code, not shell commands. The `bash` code fence is slightly misleading since these are Claude Code session commands, not terminal commands. Consider using a plain code block or adding a note.
- **Lines 53-60**: Bash command patterns (Bankr CLI, Bankr API, generic pattern) are listed clearly. Good specificity.
- **Line 65**: Note about keyword matching vs. semantic analysis is important. Good callout.
- **Line 93**: `npx @mandate.md/cli login --name "claude-agent"` is the registration step. Clear.
- **Line 139**: "Mandate's own tools are always allowed" section prevents confusion about recursive blocking.

## Developer Experience Notes

Very strong page. The two-phase gate explanation is the highlight: a developer immediately understands why their transaction was blocked and what to do about it. The example flow (lines 104-131) walks through a complete happy path and a block path.

Two minor DX concerns:
1. The install commands (lines 20-21) look like bash but are actually Claude Code session commands. A developer copying these into a terminal will get errors. Adding "Run these inside Claude Code:" before the code block would prevent confusion.
2. There is no tools/actions table in the formal sense. The page describes gate triggers in prose (lines 53-60), which works but is harder to scan than a table. Adding a summary table of "what triggers the gate" vs. "what passes through" would improve scannability.

## Score

**8.5 / 10**
