# QA Report: sdk/types.mdx

## Checklist

| # | Rule | Pass/Fail |
|---|------|-----------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | FAIL (no "## Next Steps" heading) |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline link to /sdk/intent-hash at line 176) |
| 7 | Correct terminology | PASS |
| 8 | Code examples: imports, realistic names, TS correct | PASS |
| 9 | Types complete: all fields documented, descriptions accurate | PASS |

## Findings

### F1. Missing "## Next Steps" heading before CardGroup (line 289)

The CardGroup at the bottom has no `## Next Steps` heading above it. The writing guide template requires this heading.

### F2. No "What is" opening paragraph

The page starts with "Every type listed here is exported from `@mandate.md/sdk`:" without a definition-first paragraph. Adding a brief "What are the SDK types?" section would improve LLM citability per the GEO optimization rules.

### F3. `PreflightResult` extends `ValidateResult` (line 97)

The `extends ValidateResult` relationship is noted but the field table on lines 102-111 repeats all `ValidateResult` fields. This is developer-friendly (no jumping between sections), but a note clarifying the inheritance would help TypeScript developers understand the type hierarchy.

### F4. `Hash` type in `TransferResult` not explained (line 277)

Line 277: `txHash: Hash;` -- The `Hash` type is from viem. This is explained in the field table (line 285: "viem `Hash` type, which is `` `0x${string}` ``"), which is good. No issue.

### F5. `ExternalSigner.sendTransaction` parameter types use `bigint` (line 249-256)

The `value`, `gas`, `maxFeePerGas`, `maxPriorityFeePerGas` fields use `bigint`, while `IntentPayload` uses `string` for similar fields (`valueWei`, `gasLimit`, etc.). This type inconsistency between the two interfaces is not explained. A developer might wonder why one uses strings and the other bigints. A brief note would help.

### F6. All interfaces have both code blocks and field tables

Every type has: (1) the TypeScript interface definition, (2) a markdown table with Type, Required (where applicable), and Description columns. This consistent structure is excellent for scanning.

### F7. Missing link to /reference/block-reasons for `blockReason` fields

The `blockReason` field appears in `ValidateResult`, `PreflightResult`, and `IntentStatus`, but none of the field descriptions link to the block reasons reference. Adding a link on at least one occurrence would help developers discover the full list.

## Developer Experience Notes

- **Excellent:** Every type is fully documented with both code block and field table. A developer can use this as a complete reference without reading source code.
- **Excellent:** The import block at the top (lines 9-21) shows all exportable types in one place. Developers can copy what they need.
- **Good:** The `ExternalSigner` documentation explains which fields are optional and why ("some signers manage these internally").
- **Good:** Types are ordered logically: config types first, then request types, then response types, then utility types.
- **Gap:** No explanation of why `IntentPayload` uses string types for numeric values while `ExternalSigner` uses bigint. This is confusing for developers working with both interfaces.
- **Gap:** No `type` import guidance for developers who want to import types only (e.g., `import type { ... }`). The top example uses `import type` which is correct, but no note about why this is preferred.
- **Minor:** `PreflightPayload.amount` is described as "Human-readable amount (e.g. `'5.00'`)" but in the `mandate-client.mdx` example (line 33), it uses `'50'` without decimals. The two pages are consistent enough, but the `.00` suffix in the example value could mislead.

## Score

**8.5 / 10** -- Comprehensive type reference with consistent structure. Every interface is documented with both code and tables. Missing the "Next Steps" heading, lacks cross-links to block reasons reference, and the string-vs-bigint inconsistency between interfaces is unexplained.
