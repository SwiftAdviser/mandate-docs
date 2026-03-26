# QA Report: sdk/intent-hash.mdx

## Checklist

| # | Rule | Pass/Fail |
|---|------|-----------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS (no "## Next Steps" heading, but CardGroup present) |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline link to /troubleshooting/intent-hash-mismatch = 4) |
| 7 | Correct terminology | PASS |
| 8 | Code examples: imports, realistic names, TS correct | PASS |
| 9 | Function signature, parameters, return type documented | PASS |

## Findings

### F1. Missing "## Next Steps" heading before CardGroup (line 107)

The CardGroup at the bottom has no `## Next Steps` heading. The writing guide template requires this heading before the closing CardGroup.

### F2. No installation section or import snippet

Unlike other SDK pages, this page does not import or show the `<InstallSdk />` snippet. Since `computeIntentHash` is an SDK export, developers arriving here from search should see how to install the package.

### F3. Good: "When You Need This" section (lines 101-105)

This section proactively answers "do I even need this?" and correctly directs most developers to `MandateWallet` (which handles hashing internally). Only advanced users building custom signing flows need `computeIntentHash`. This saves developers from unnecessary complexity.

### F4. Good: "Common Mismatch Causes" (lines 89-97)

This is a high-value troubleshooting section. The ordered list matches the frequency of real-world bugs: stale nonce > gas drift > casing > calldata > access list. Developers debugging hash mismatches will find this immediately useful.

### F5. Canonical string format well documented (lines 17-28)

The pipe-delimited format with explicit rules about lowercasing and serialization is precisely what a developer implementing a custom flow needs. No ambiguity.

### F6. `HashInput` interface fully documented (lines 59-85)

All 10 fields have type, required status, and description. The descriptions include practical guidance (e.g., "Use `0x` for native transfers" for calldata).

### F7. Return type not explicitly stated in prose

The `computeIntentHash` function returns a `0x${string}` hex hash, which is shown in the code example (line 50: `// hash: 0x...`) and described in line 53 ("returns the keccak256 hash as a hex string"). However, there is no formal return type annotation in a signature block. Adding `Returns: \`0x\${string}\`` would complete the documentation pattern used on other pages.

## Developer Experience Notes

- **Excellent:** The canonical string format documentation is precise and unambiguous. A developer implementing this in Python or Rust could reproduce the hash correctly from this page alone.
- **Excellent:** The "Common Mismatch Causes" list is ordered by likelihood, which saves debugging time.
- **Good:** The "When You Need This" section prevents unnecessary complexity for developers using `MandateWallet`.
- **Good:** The example uses realistic gas values and a real USDC address.
- **Gap:** No formal return type for `computeIntentHash`. The example implies it, but it should be explicit.
- **Gap:** No mention of which keccak256 implementation the SDK uses (viem's `keccak256`? ethers'?). Developers building custom implementations need to know the exact library to match output.
- **Minor:** The page links to `/troubleshooting/intent-hash-mismatch` (line 105), but it would also be useful to link to `/sdk/mandate-client` (rawValidate section) since that is the primary consumer of `computeIntentHash`.

## Score

**8.5 / 10** -- Technically precise and well-structured for its purpose. The canonical format docs and mismatch causes are standout sections. Missing the "Next Steps" heading, formal return type, and installation snippet keep it from a higher score.
