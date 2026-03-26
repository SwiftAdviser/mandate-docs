# QA Report: cli/llms-flag.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline link to llms.txt standard) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PARTIAL |

## Findings

- **Line 9-10**: Opening explains the purpose and links to the llms.txt standard. Good context.
- **Line 12-14**: Both flags shown. "No authentication required. No side effects." Reassuring for an agent exploring.
- **Line 18-31**: Compact manifest example shows all 8 commands with `next` pointers. Matches the overview's command table.
- **Line 33**: "Each entry includes a next field" reinforces the chaining pattern.
- **Line 37**: "Returns the full command manifest with option schemas, argument types, defaults, and usage examples." Clear feature description.
- **Line 39-44**: Bullet list of what the full manifest includes. Five items covering schemas, types, examples.
- **Line 48-54**: "How agents use this" section is a 4-step discovery flow. Good for AI agent developers.
- **Line 57-59**: Tip pointing to SKILL.md for the complete API reference. Good cross-link.

## Developer Experience Notes

- **Agent-oriented page**: This page is written for AI agent developers, not end users. The "How agents use this" section (lines 48-54) gives a concrete workflow.
- **Missing**: No actual `--llms-full` output example. The compact manifest is shown (lines 22-30), but the full manifest is only described in prose (lines 39-44). A developer (or agent) would benefit from seeing a truncated example of the full output, even one command's worth.
- **Missing**: No mention of the output format. Is it JSON? YAML? Plain text? The compact example (lines 22-30) looks like plain text, but a developer parsing it programmatically needs to know the format.
- **Minor**: The compact manifest example (lines 22-30) does not look like structured data. It appears to be human-readable text. If the actual output is structured JSON or YAML, the example is misleading.

## Score

**7/10**

Good conceptual page. Missing a `--llms-full` output example and format specification. A developer trying to parse the output needs to know the data format.
