# QA Report: dashboard/policy-builder.mdx

## Checklist

| # | Rule | Pass? |
|---|------|-------|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 3 inline = 6) |
| 7 | Correct terminology | PASS |
| 8 | UI elements clearly described, step-by-step actions | PASS |

## Findings

### PASS: All structural checks pass
Frontmatter complete. No em dashes. No filler words. Terminology correct. 6 cross-links total (3 inline: policy engine, approval queue, MANDATE.md editor; 3 cards).

### GOOD: Comprehensive field coverage
Covers spend limits, allowed addresses, allowed contracts, blocked selectors, blocked actions, approval requirements, gas/value caps, schedule, guard rules, and policy versioning. Each section maps to a dashboard form area.

### GOOD: Popular token shortcuts (lines 36-42)
Practical detail about quick-add buttons for USDC/USDT. This is exactly the kind of dashboard-specific UI detail that helps users.

### GOOD: Policy versioning warning (lines 101-103)
Critical operational detail: saving takes effect immediately. The Warning callout is appropriate here.

### MINOR: "Blocked selectors" section assumes knowledge (line 46)
Line 46 mentions "4-byte function selectors (hex)" without explaining how to find them. A link to a selector database (e.g., 4byte.directory) or a Tip callout would help developers who don't know the selector for `approve()`.

### MINOR: No screenshot references
The policy builder is described as "the most important page in the Mandate dashboard" (line 9). A screenshot or annotated image of the form would be valuable, especially for the schedule multiselect and the guard rules text field.

### NOTE: Schedule section is light (lines 78-81)
"Configure allowed days (Monday through Sunday) and hours (0-23) using the multiselect controls" is a single sentence. Timezone handling is not mentioned. Are hours in UTC? Local time? This is a common source of confusion.

## Developer Experience Notes

- This is the densest page in the dashboard docs. It covers a lot of ground clearly.
- The separation between "what this field does" and "how the policy engine evaluates it" is well-maintained. Links to the policy engine concept page carry the deeper explanation.
- Missing: what happens when I save a policy with conflicting rules? (e.g., "allow transfers" in guard rules but "block transfer" in blocked actions). Is there a validation step?
- Missing: how to reset a policy to defaults or clear all fields.
- The guard rules example (lines 89-93) is helpful but short. The link to the MANDATE.md editor page provides more examples, so this is acceptable.
- Would benefit from a "Policy builder walkthrough" subsection with numbered steps: 1. Select agent, 2. Set limits, 3. Add addresses, 4. Save.

## Score

**8.5/10** - Comprehensive and well-linked. The most important dashboard page gets thorough treatment. Loses half a point for missing timezone info on schedules and no screenshot references. Minor improvements to the blocked selectors section and a first-time walkthrough would bring it to 9+.
