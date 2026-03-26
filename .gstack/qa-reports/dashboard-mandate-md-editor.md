# QA Report: dashboard/mandate-md-editor.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline = 4) |
| 7 | Correct terminology | PASS |
| 8 | UI elements clearly described, step-by-step actions | PASS |

## Findings

### PASS: All structural checks pass
Clean frontmatter, no em dashes, no filler words, correct terminology. 4 cross-links total.

### GOOD: Step-by-step "How it works" (lines 13-18)
Clear 4-step numbered workflow: select agent, write rules, check preview, save. This is the kind of step-by-step guidance dashboard docs need.

### GOOD: Three realistic examples (lines 28-57)
DeFi trader, payroll bot, and shopping agent examples are excellent. They show concrete rules with specific dollar values that map to real use cases. Developers can copy-paste and adapt these.

### GOOD: Preview panel section (lines 59-70)
Enumerates what the preview shows and explains the amber highlight for unparseable rules. This reduces confusion when rules don't map as expected.

### GOOD: Comparison table (lines 76-81)
Clear side-by-side of MANDATE.md editor vs policy builder. Answers "when should I use which?" directly.

### MINOR: No error handling guidance
Line 70 mentions rules that "cannot be parsed" get highlighted in amber, but there's no guidance on common parsing failures. What patterns commonly fail? What if a rule is partially parsed?

### MINOR: No mention of syntax highlighting or keyboard shortcuts
The editor is described as a text field but no mention of whether it has syntax highlighting, line numbers, or keyboard shortcuts (Ctrl+S to save, etc.). These details matter for a text editing experience.

### NOTE: The real-time preview (line 18) is a strong UX feature
Worth emphasizing more. "Preview updates in real time" is buried in a paragraph. Consider making it more prominent.

## Developer Experience Notes

- This is one of the most user-friendly pages in the dashboard docs. The examples are the standout feature.
- The three use cases (DeFi trader, payroll bot, shopping agent) cover different archetypes well. A fourth example for a "monitoring/read-only agent" that only needs view permissions would round out coverage.
- Missing: versioning. When I save from the MANDATE.md editor, does it create a new policy version like the policy builder does? The policy builder page mentions versioning but this page doesn't.
- Missing: import/export of MANDATE.md files. Can I write the file locally in my repo and sync it to the dashboard? The name "MANDATE.md" implies it could be a file in a git repo.
- Missing: collaboration. Can two people edit the same agent's rules simultaneously? What happens?
- The character limit section (lines 85-87) is practical but could mention what 10,000 characters translates to in rule count (roughly).

## Score

**9/10** - The strongest dashboard page in the set. Excellent examples, clear workflow, and good comparison table. Minor gaps in error handling guidance and versioning mention. The examples alone make this page highly useful for new users.
