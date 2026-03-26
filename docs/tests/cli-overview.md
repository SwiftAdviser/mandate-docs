# QA Report: cli/overview.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 9**: Opening paragraph is 49 words. Dense but within bounds. Covers what the CLI is and what it does. Good for LLM citation.
- **Line 42-53**: Command table is clear and complete. Auth column is a nice touch.
- **Line 56-69**: Credential storage section shows the JSON file structure. Useful for debugging.
- **Line 71-73**: Warning about not committing credentials. Good security callout.
- **Line 80-81**: `--llms` and `--llms-full` flags shown with brief explanation. Links to dedicated pages would improve discoverability, but the dedicated pages exist separately.
- **Line 98**: CardGroup uses `cols={3}`. Writing guide example uses `cols={2}`. Not a violation, but inconsistent with most other pages.

## Developer Experience Notes

- **Install section** (lines 11-38): Clear. Shows both `npx` and global install with bun/npm tabs. The first real command example (line 37) is a full `validate` invocation, which is great for copy-paste.
- **Command table**: All 9 commands listed with auth requirements. I can scan this in seconds to find what I need.
- **Missing**: No mention of `--help` flag or version check (`--version`). A developer's first instinct is often `mandate --help`, and confirming the install worked via `mandate --version`.
- **Missing**: No link to `--llms` or `--mcp` dedicated pages from the command table or body text. These are documented in the Agent Discovery and MCP sections (lines 77-94) but the command table only lists the 9 "real" commands. A developer looking for `--llms` in the table won't find it.

## Score

**9/10**

Minor gaps: no `--help`/`--version` mention, and the `--llms`/`--mcp` flags are explained in prose but not linked to their dedicated reference pages.
