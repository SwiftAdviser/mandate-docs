# QA Report: sdk/overview.mdx

## Checklist

| # | Rule | Pass/Fail |
|---|------|-----------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | FAIL |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (4: 3 cards + 1 inline to /sdk/errors) |
| 7 | Correct terminology | PASS |
| 8 | Code examples: imports, realistic names, TS correct | PASS |
| 9 | Method signatures complete, params documented, return types shown | N/A (overview page) |

## Findings

### F1. Long paragraph (line 81)

**Line 81:** "Every failure mode has a dedicated error class. Your agent catches `PolicyBlockedError` for policy violations, `ApprovalRequiredError` when human review is needed, `CircuitBreakerError` when the agent is emergency-stopped, and `RiskBlockedError` when the risk scanner flags the transaction. All extend `MandateError`, so you can catch the base class as a fallback. See [Error Handling](/sdk/errors) for patterns and examples."

This is 4 sentences, which is at the boundary. Technically passes, but the second sentence is very long with four clauses. Consider splitting it into two sentences.

### F2. "PreflightResult" type name in prose (line 46)

Line 46 says: "you get back a `PreflightResult` with `allowed: true`". The type is called `PreflightResult` (which uses "Preflight" in its name), but this is an SDK type name, not prose terminology. Acceptable, but worth noting the naming inconsistency with the "validate" terminology preference. The writing guide says "preflight" is allowed "when explaining the alias", and here it is the actual type name.

### F3. No "definition first" (60-word opener)

Line 9-11: The opening answers "What is the Mandate SDK?" in one long sentence (~57 words). This passes the 60-word target.

## Developer Experience Notes

- **Good:** The page gives a complete picture of what the SDK exports, with a clear table of all named exports. A developer scanning this page knows exactly what classes and functions are available.
- **Good:** The sub-path import tip (line 67-77) is valuable for bundle-conscious projects. This is non-obvious and saves developers from discovering it later.
- **Good:** Quick start example (line 21-43) shows imports, error handling, and realistic variable names. A developer can copy-paste and run.
- **Minor gap:** The quick start uses `process.env.MANDATE_RUNTIME_KEY!` but does not mention which env var name to set. A developer new to the SDK might wonder if `MANDATE_RUNTIME_KEY` is a convention or required.
- **Minor gap:** No mention of minimum Node.js version or TypeScript version requirements.

## Score

**8.5 / 10** -- Solid overview page. Clean structure, good exports table, functional quick start. Minor gaps in environment setup context and one borderline-long paragraph.
