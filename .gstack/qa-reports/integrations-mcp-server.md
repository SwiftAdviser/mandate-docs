# QA Report: integrations/mcp-server.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards -- minimum threshold) |
| 7 | Terminology compliance | PASS |
| 8 | Install/deploy command shown | PASS (lines 24-29) |
| 9 | Configuration steps clear | PASS (env vars table lines 45-48, client config lines 52-74) |
| 10 | Code example complete | PASS (deploy, dev, client config, inspector) |
| 11 | Tools/actions table present | PASS (lines 15-18) |

## Findings

No violations found.

- Lines 24-29: Deploy steps are clear: cd, install, set secret, deploy. Four commands.
- Lines 35-39: Local dev section shows `bun run dev` and documents the endpoints (`/sse` and `/mcp`). Good for testing.
- Lines 52-74: Three client configuration examples (Claude Desktop, Codex CLI, Cursor/Windsurf). Each uses the correct format for that client. The Claude Desktop JSON and Codex TOML examples are copy-paste ready.
- Line 74: Cursor/Windsurf section says "Add the SSE URL in your editor's MCP settings" without a concrete example. Less helpful than the other two, but reasonable since editor UIs vary.
- Line 91: `npx @mandate.md/cli --mcp` alternative is documented. Good for developers who do not want Cloudflare Workers.
- Line 97: Note about stateless design is important for understanding the architecture.

## Developer Experience Notes

Good page for a deployment-oriented integration. The four-step deploy (lines 24-29) gets a developer to a running MCP server quickly. The three client configuration sections cover the main MCP clients.

The `search` tool description (line 17) is useful: it tells developers to call `search` before `execute` to learn the request format. This is a good onboarding pattern.

Minor gap: no error handling section. What happens when `execute` fails? What does the MCP tool return on a policy block? Other integration pages show block and approval responses. A developer building an MCP client would benefit from seeing example responses.

The alternative CLI MCP mode (lines 88-94) is a strong addition. It gives developers a local option without requiring Cloudflare Workers infrastructure.

## Score

**8 / 10**
