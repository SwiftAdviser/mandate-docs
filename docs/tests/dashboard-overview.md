# QA Report: dashboard/overview.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | FAIL |
| 7 | Correct terminology | FAIL |
| 8 | UI elements clearly described, step-by-step actions | WARN |

## Findings

### FAIL: Only 2 cross-links (line 45-51)
The Next Steps section has only 2 cards (Agents, Policy Builder). The writing guide requires 3-5 cross-links. Missing obvious targets: Approvals, Audit Log, or Quickstart.

### FAIL: Banned term "transaction requests" (line 25)
Line 25: `Review and act on pending transaction requests`. Should be "intents" per the terminology table.

### WARN: No screenshot reference
The dashboard home page is a visual-first experience. The "Dashboard home" section (line 39-40) describes metrics at a glance but never references a screenshot. A screenshot or annotated image would help new users orient themselves.

### WARN: "Agent activation prerequisite" section lacks step-by-step
Line 31-36 describes a prerequisite but doesn't give explicit steps. A user stuck on this limited view would benefit from: 1. Go to Agents, 2. Create an agent, 3. Set wallet address. The Tip callout partially addresses this but remains vague.

### NOTE: Navigation table is strong (line 19-28)
Clean mapping of sidebar sections to purposes. Good quick reference.

## Developer Experience Notes

- The page works as a landing/orientation page. It answers "what is this" and "where do I go" quickly.
- Missing: any mention of team/org features. If I manage agents with a team, does each person get their own dashboard? No clarity.
- Missing: keyboard shortcuts or search functionality mention. Power users managing 10+ agents need fast navigation.
- The "Sign in" section is helpful but brief. No mention of what happens if GitHub org membership is required or how permissions work.
- The navigation table is the strongest part. Consider linking each row to its respective page.

## Score

**7/10** - Solid orientation page. Loses points for insufficient cross-links and a terminology violation. Adding 1-2 more cards and fixing "transaction requests" to "intents" would bring it to compliance.
