# QA Report: sdk/errors.mdx

## Checklist

| # | Rule | Pass/Fail |
|---|------|-----------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards in CardGroup) |
| 7 | Correct terminology | PASS ("emergency stop" on line 99 is acceptable in explanations per writing guide) |
| 8 | Code examples: imports, realistic names, TS correct | PASS |
| 9 | Error classes complete: properties, when-it-fires, recovery, example | PASS |

## Findings

### F1. No "What is" opening section

The writing guide says concept pages should open with "What is X?" answered in the first 60 words (GEO/LLM optimization rule 1). This page jumps straight into "Class Hierarchy" without a brief intro paragraph. A one-sentence opener like "The Mandate SDK uses five typed error classes to represent every failure mode your agent can encounter" would improve LLM citability.

### F2. Missing `<Note>` section header "## Next Steps"

Line 223 jumps directly from the "Instanceof Checking Pattern" code block to the `<CardGroup>`. There is no `## Next Steps` heading above the CardGroup. The writing guide template shows this heading is required.

### F3. Cross-links at minimum (3)

The page has exactly 3 card links: /guides/handle-errors, /reference/block-reasons, /sdk/mandate-client. This meets the minimum of 3, but the writing guide says 3-5. Adding links to /sdk/mandate-wallet and /sdk/types would improve navigation.

### F4. `PolicyBlockedError` example missing `reason` in transfer call (line 77)

```typescript
await wallet.transfer(to, amount, tokenAddress);
```

The `transfer()` method requires a `reason` via opts. This example omits it, which would cause a runtime error if copy-pasted. Should be:

```typescript
await wallet.transfer(to, amount, tokenAddress, { reason: 'Payment' });
```

### F5. `CircuitBreakerError` example also missing `reason` (line 113)

Same issue. The `wallet.transfer()` call omits the reason parameter.

### F6. `RiskBlockedError` example also missing `reason` (line 177)

Same pattern. All three wallet.transfer examples in the individual error sections omit the `reason` opts.

### F7. Good: "Instanceof Checking Pattern" section (lines 188-221)

This section answers the natural question "how do I handle all error types together?" and gets the ordering right (specific before base). The comment on line 190 ("Order matters: check specific subclasses before the base `MandateError`") is valuable.

### F8. Good: Each error has "When it fires" and "Recovery" sections

This is excellent structure. A developer debugging a production error can quickly find their error class, understand the trigger, and know the recovery path.

## Developer Experience Notes

- **Excellent:** The "When it fires" / "Recovery" pattern for each error class is exactly what a developer needs when debugging. No hunting through prose.
- **Excellent:** The instanceof checking pattern with ordering guidance prevents a subtle bug (base class catching before subclass).
- **Good:** Property tables for each error class are complete with types and descriptions.
- **Bug:** Three code examples omit the required `reason` parameter in `wallet.transfer()`. A developer copy-pasting these will get a runtime error.
- **Gap:** No mention of what happens with network errors (e.g., Mandate API unreachable). Does it throw `MandateError`? A plain `Error`? This is a critical production scenario.
- **Gap:** No guidance on retry logic for `MandateError` with 5xx status codes. The recovery section says "5xx errors are transient and safe to retry with backoff" but does not show a retry pattern.

## Score

**8.0 / 10** -- Strong error reference with excellent structure per error class. The instanceof pattern section is a highlight. Loses points for missing `reason` in three code examples (copy-paste hazard), missing "Next Steps" heading, and no coverage of network error scenarios.
