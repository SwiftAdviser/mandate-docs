# QA Report: cli/mcp-flag.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 2 inline links: /integrations/claude-code, /integrations/mcp-server) |
| 7 | Correct terminology | PASS |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 9**: Opening explains stdio transport, MCP protocol link, and the key constraint: "No HTTP server, no port binding." Good.
- **Line 17-23**: Exposed tools table is clear. Two tools: `search` (read-only, no auth) and `execute` (needs runtime key). The distinction is important.
- **Line 29-46**: Claude Desktop config is a complete, copy-paste JSON block with the correct file paths for macOS and Windows.
- **Line 48-62**: Codex CLI config is clean. TOML format, env var for the runtime key.
- **Line 64-72**: Claude Code section shows both the `claude mcp add` command and links to the dedicated plugin page. Good.
- **Line 74-83**: "How it works" section is a 4-step numbered list. Clear internal flow.
- **Line 85-89**: "When to use MCP vs the CLI directly" section answers the obvious question. Good.
- **Line 91-93**: Note linking to the cloud-hosted MCP server alternative. Important for teams that don't want local processes.

## Developer Experience Notes

- **Three client configurations**: Claude Desktop, Codex CLI, Claude Code. Covers the major AI assistant use cases. Each has a copy-paste config block.
- **The search vs execute distinction (lines 17-23)**: A developer knows that discovery works without auth, but execution needs a key. This prevents confusion during setup.
- **Missing**: No example of what a tool call looks like from the assistant's perspective. Showing a sample MCP tool invocation and response would help developers test their setup.
- **Missing**: No troubleshooting. What if the MCP server fails to start? What if the runtime key is missing? A brief "Common issues" section would help.
- **Minor**: Line 46 mentions Windows path but the docs seem primarily macOS/Linux-oriented. Consistency is good.

## Score

**9/10**

Strong page. Three client configs with copy-paste blocks. Good conceptual framing (MCP vs CLI). Missing a tool call example and troubleshooting section.
