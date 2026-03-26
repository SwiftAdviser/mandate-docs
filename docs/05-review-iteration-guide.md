# Review and Iteration Guide

Use this document when reviewing or updating the documentation.

## How to make changes

1. Edit MDX files in the `SwiftAdviser/mandate-docs` repo
2. Push to `master`
3. Mintlify auto-deploys in ~30 seconds

## Local preview

```bash
cd ~/Projects/mandate-docs
npx mintlify dev
# Opens localhost:3000
```

## File structure

```
mandate-docs/
  docs.json              # Navigation, colors, navbar, footer, features
  openapi.json           # OpenAPI 3.1 spec (powers API Reference tab)
  WRITING-GUIDE.md       # Style rules for all articles
  snippets/              # 7 reusable MDX blocks
  introduction.mdx       # Landing page
  quickstart.mdx         # 4-path quickstart
  how-it-works.mdx
  concepts/              # 7 deep concept pages
  guides/                # 9 task-oriented guides
  sdk/                   # 7 SDK reference pages
  cli/                   # 12 CLI command pages
  api-reference/         # 1 overview (rest auto-generated from openapi.json)
  integrations/          # 10 integration guides
  dashboard/             # 10 dashboard feature pages
  security/              # 7 security pages
  reference/             # 7 lookup tables
  troubleshooting/       # 5 troubleshooting pages + FAQ
  llms-skill.mdx         # SKILL.md for AI agents
  changelog.mdx
  docs/                  # This meta-documentation
```

## Adding a new page

1. Create the `.mdx` file in the right directory
2. Add frontmatter: title, sidebarTitle, description
3. Add the page path to `docs.json` navigation (in the correct tab/group)
4. Add 3-5 cross-links to related pages
5. Add "Next Steps" CardGroup at the bottom
6. Follow WRITING-GUIDE.md rules

## Adding a new integration

1. Create `integrations/<name>.mdx`
2. Add to `docs.json` under Integrations > Agent Frameworks > pages
3. Add to the comparison matrix in `integrations/overview.mdx`
4. Add to the quickstart resources table if it's a primary channel
5. Structure: What is it, Install, Usage (code), Tools/Actions table, Config, Error handling, Next Steps

## Updating the OpenAPI spec

1. Edit `openapi.json`
2. Endpoints listed in `docs.json` navigation under "Agent API" and "Dashboard API" auto-generate pages
3. Use `"openapi": "/openapi.json"` on the group to link them
4. Format: `"POST /api/validate"` (method + path as the page identifier)

## Updating the SKILL.md mirror

The `llms-skill.mdx` page mirrors `public/SKILL.md` from the main mandate repo. When SKILL.md changes:
1. Read the updated `public/SKILL.md`
2. Update `llms-skill.mdx` to reflect changes
3. Keep the condensed, structured format (tables, minimal prose)

## Key pages to keep in sync with code

| Documentation page | Source of truth |
|-------------------|----------------|
| `sdk/mandate-client.mdx` | `packages/sdk/src/MandateClient.ts` |
| `sdk/mandate-wallet.mdx` | `packages/sdk/src/MandateWallet.ts` |
| `sdk/types.mdx` | `packages/sdk/src/types.ts` |
| `sdk/errors.mdx` | `packages/sdk/src/types.ts` (error classes) |
| `cli/*.mdx` | `packages/cli/src/commands/*.ts` |
| `reference/block-reasons.mdx` | `app/Services/PolicyEngineService.php` |
| `reference/policy-fields.mdx` | `database/migrations/*policies*` |
| `reference/intent-states.mdx` | `app/Models/TxIntent.php` |
| `concepts/policy-engine.mdx` | `app/Services/PolicyEngineService.php` |
| `api-reference/overview.mdx` + `openapi.json` | `routes/api.php` |
| `llms-skill.mdx` | `public/SKILL.md` |
| `reference/chain-reference.mdx` | `packages/sdk/src/index.ts` (USDC, CHAIN_ID) |

## Review checklist for any page

- [ ] Frontmatter has title, sidebarTitle, description
- [ ] No em dashes (use colons, periods, commas)
- [ ] No filler words (simply, just, easily, leverage)
- [ ] Short paragraphs (2-4 sentences)
- [ ] Code examples show imports and use realistic values
- [ ] 3-5 cross-links to related pages
- [ ] CardGroup "Next Steps" at bottom
- [ ] Terminology matches glossary (runtime key, not API key, etc.)
- [ ] Concept pages open with "What is X?" in first 60 words
- [ ] Code tabs order: TypeScript SDK, CLI, curl

## Review checklist for the full site

- [ ] `docs.json` is valid JSON
- [ ] `openapi.json` is valid JSON
- [ ] Every page in docs.json navigation has a corresponding .mdx file
- [ ] No broken internal links (run `npx mintlify dev` to check)
- [ ] llms.txt accessible at /llms.txt
- [ ] Quickstart reflects all current distribution channels
- [ ] Block reasons match PolicyEngineService.php
- [ ] Intent states match TxIntent.php
- [ ] Policy fields match migrations
- [ ] SDK method signatures match source code

## Common iteration tasks

### Add a new CLI command
1. Create `cli/<command>.mdx` with frontmatter
2. Add to `docs.json` under SDK > CLI > pages
3. Add to `cli/overview.mdx` command table

### Add a new block reason
1. Add to `reference/block-reasons.mdx` table
2. Add to `troubleshooting/common-errors.mdx` if common
3. Update `concepts/policy-engine.mdx` check table if new check

### Add a new chain
1. Add to `reference/chain-reference.mdx` table
2. Add to `sdk/constants.mdx` USDC and CHAIN_ID tables
3. Update `llms-skill.mdx` chain reference section
4. Update `troubleshooting/faq.mdx` chain support Q&A

### Add a new approval trigger
1. Add to `reference/approval-triggers.mdx` table
2. Update `concepts/policy-engine.mdx` if it's a new check
3. Update `guides/handle-approvals.mdx` trigger list

## Links

| Resource | URL |
|----------|-----|
| Live docs | https://docs.mandate.md |
| GitHub repo | https://github.com/SwiftAdviser/mandate-docs |
| Mintlify dashboard | https://dashboard.mintlify.com |
| Mintlify docs | https://mintlify.com/docs |
| Main mandate repo | https://github.com/SwiftAdviser/mandate (private) |
| Claude Code plugin | https://github.com/SwiftAdviser/claude-mandate-plugin |
| OpenClaw plugin | https://github.com/SwiftAdviser/mandate-openclaw-plugin |
| Skill repo | https://github.com/SwiftAdviser/mandate-skill |
| ClawHub | https://clawhub.ai/swiftadviser/mandate |
| npm SDK | https://www.npmjs.com/package/@mandate.md/sdk |
| npm CLI | https://www.npmjs.com/package/@mandate.md/cli |
| Telegram community | https://t.me/mandate_md_chat |
