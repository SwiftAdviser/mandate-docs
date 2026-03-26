# QA Report: integrations/vercel-ai.mdx

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
| 8 | Install command shown | FAIL -- no install command |
| 9 | Configuration steps clear | PARTIAL -- no env var table or config breakdown |
| 10 | Code example complete | PASS (lines 15-37, shows imports, init, validate, error catch) |
| 11 | Tools/actions table present | FAIL -- no tools/actions table |

## Findings

- **Line 8**: "Coming soon" Info callout is appropriate. However, the page is published and discoverable, so it should still meet minimum quality for the interim approach.
- **Missing install command**: The page shows `import { MandateClient, PolicyBlockedError } from '@mandate.md/sdk'` but never shows `bun add @mandate.md/sdk` or any install step. A developer following this page must guess the package name or navigate to the SDK overview page.
- **Missing tools/actions table**: Since this is an interim "use the SDK directly" page, there are no framework-specific tools to document. However, a short table showing what the developer gets (e.g., `MandateClient.validate()`, `PolicyBlockedError`) would meet the spirit of the rule.
- **Missing env var / config table**: No `MANDATE_RUNTIME_KEY` environment variable documentation. The code uses `process.env.MANDATE_RUNTIME_KEY!` but the page never explains what this key is or how to get one.
- **Line 40**: "The `validate()` call takes less than 200ms" is a good concrete number per the writing guide's "specific numbers" rule.
- **Lines 42-44**: "What the dedicated plugin will add" section is forward-looking and sets expectations. Good.
- **Line 17**: `import { generateText } from 'ai'` is imported but never used in the example. Dead import.

## Developer Experience Notes

This is the weakest integration page. A developer who wants to add Mandate to a Vercel AI SDK project hits several friction points:

1. No install command. They have to figure out the package name from the import statement.
2. No env var documentation. `MANDATE_RUNTIME_KEY` appears in code but is never explained. Where do you get it? What format? The other integration pages document this.
3. The code example imports `generateText` from `'ai'` (line 17) but never uses it. This is confusing: is it part of the pattern or a leftover?
4. No tools/actions table. What capabilities does Mandate expose to the AI? The page only shows a single `validate()` call.

The "coming soon" status is understandable, but the interim page should still be self-sufficient for a developer who wants to integrate today. Adding an install command, an env var table, and removing the unused import would significantly improve this page.

## Score

**5.5 / 10**
