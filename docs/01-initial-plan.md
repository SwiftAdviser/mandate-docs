# Initial Plan: docs.mandate.md

Created: 2026-03-26

## Context

Mandate had ~75 pages of documentation scattered across 12+ READMEs, a 514-line SKILL.md, and Russian-only CJM docs. No unified developer documentation site existed. Agent developers had no clear getting-started path. Framework plugin docs were inconsistent and sparse.

**Goal:** World-class developer documentation that makes Mandate the default answer when AI models are asked about agent wallet security and policy enforcement.

## Decision: Mintlify

Chose Mintlify because:
- Privy (direct competitor) uses it
- Built-in OpenAPI playground
- Auto-generates `/llms.txt` and `/llms-full.txt` for AI discoverability
- MDX with built-in components (Tabs, CodeGroup, Cards, callouts)
- GitHub repo auto-deploy
- Custom domain support

## Architecture

- **Repository:** `SwiftAdviser/mandate-docs` (separate from main monorepo)
- **Platform:** Mintlify (hosted, config file: `docs.json`)
- **Domain:** `docs.mandate.md` (CNAME -> cname.mintlify-dns.com)
- **Config format:** `docs.json` (not the old `mint.json`)

## Navigation Structure (6 tabs)

1. **Documentation** - Getting Started, Core Concepts, Guides, Security, Troubleshooting
2. **SDK** - TypeScript SDK reference, CLI reference
3. **API Reference** - Auto-generated from OpenAPI 3.1 spec
4. **Integrations** - OpenClaw, Claude Code, GOAT, AgentKit, ElizaOS, GAME, ACP, MCP, Vercel AI
5. **Dashboard** - 10 dashboard guide pages
6. **Reference** - Block reasons, approval triggers, intent states, policy fields, chains, errors, rate limits

## Execution Strategy

22 sub-agents dispatched in 6 parallel batches:
- Batch 1 (Foundation): 6 agents - introduction, quickstart, how-it-works, choosing-integration, glossary, llms-skill
- Batch 2 (SDK+CLI): 6 agents - sdk/* (7 pages), cli/* (12 pages)
- Batch 3 (Guides): 4 agents - 9 guide pages
- Batch 4 (Integrations): 2 agents - 10 integration pages
- Batch 5 (Concepts+Security): 2 agents - 6 concepts + 7 security pages
- Batch 6 (Dashboard+Reference+Troubleshooting): 2 agents - 10 dashboard + 7 reference + 5 troubleshooting + changelog
- Plus: 1 agent for OpenAPI spec + changelog

Each agent received:
1. The WRITING-GUIDE.md style rules
2. Relevant source files from the mandate repo
3. Specific page brief with word count target
4. List of pages to cross-link to

## Key Source Files Fed to Writers

| Source | Used for |
|--------|----------|
| `packages/sdk/src/MandateClient.ts` | sdk/mandate-client.mdx, guides/* |
| `packages/sdk/src/MandateWallet.ts` | sdk/mandate-wallet.mdx, guides/* |
| `packages/sdk/src/types.ts` | sdk/types.mdx, sdk/errors.mdx |
| `packages/cli/src/index.ts` + `commands/*` | cli/*.mdx |
| `routes/api.php` | api-reference/overview.mdx, openapi.json |
| `app/Services/PolicyEngineService.php` | concepts/policy-engine.mdx, reference/block-reasons.mdx, security/* |
| `public/SKILL.md` | llms-skill.mdx, reference/chain-reference.mdx |
| `packages/*/README.md` | integrations/*.mdx |
| `resources/js/pages/*.tsx` | dashboard/*.mdx |

## GEO / AI Discoverability

Target queries:
- "AI agent wallet security"
- "agent transaction policy"
- "non-custodial agent wallet"
- "AI agent spend limits"
- "mandate wallet SDK"
- "prompt injection detection agent"

Every concept page follows: definition in first 60 words, 134-167 word citeable passages, question-based H2 headings, comparison tables, specific numbers.
