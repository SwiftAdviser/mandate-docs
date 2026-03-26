# Documentation Testing Guide: Sub-Agent Methodology

How to test and validate documentation pages using parallel sub-agents.

## Overview

This guide describes a systematic approach to validating documentation quality
using one sub-agent per logical section. Each agent reads every page in its
section, checks it against the WRITING-GUIDE.md rules, and writes a structured
findings report per page.

## Architecture

```
Orchestrator (main agent)
  |
  +-- reads WRITING-GUIDE.md, docs.json, docs/*.md for context
  +-- creates /docs/tests/ output directory
  +-- writes this guide
  |
  +-- launches N parallel sub-agents (one per section):
  |     |
  |     +-- [top-level] introduction, quickstart, how-it-works, llms-skill, changelog
  |     +-- [concepts]  7 concept pages
  |     +-- [guides]    9 guide pages + choosing-integration
  |     +-- [security]  7 security pages
  |     +-- [troubleshooting] 5 troubleshooting pages
  |     +-- [sdk]       7 SDK reference pages
  |     +-- [cli]       12 CLI command pages
  |     +-- [integrations] 10 integration pages
  |     +-- [dashboard] 10 dashboard pages
  |     +-- [reference] 7 reference table pages
  |     +-- [snippets]  6 snippet files
  |
  +-- aggregates results into SUMMARY.md
```

## Validation Checklist (per page)

Each sub-agent checks every page against these rules, derived from
WRITING-GUIDE.md and docs/05-review-iteration-guide.md:

### 1. Frontmatter (required)
- [ ] Has `title` field
- [ ] Has `sidebarTitle` field
- [ ] Has `description` field
- [ ] Description is one sentence, action-oriented

### 2. Voice and Tone
- [ ] No em dashes: the character U+2014 must not appear anywhere
- [ ] No filler words: simply, just, easily, leverage, utilize, seamlessly, robust
- [ ] Active voice, present tense, second person ("you")
- [ ] Short paragraphs: 2-4 sentences max

### 3. Structure
- [ ] "Next Steps" CardGroup at the bottom of the page
- [ ] 3-5 cross-links to related pages (inline or in cards)
- [ ] Concept pages open with "What is X?" answered in the first 60 words

### 4. Code Examples
- [ ] Code blocks show imports
- [ ] Realistic variable names (not `foo`, `bar`, `key`)
- [ ] CodeGroup tabs in order: TypeScript SDK, Python, CLI, curl (when multiple)
- [ ] Example values use the approved placeholders from WRITING-GUIDE.md

### 5. Terminology
- [ ] "runtime key" not "API key" or "secret key" or "auth token"
- [ ] "validate" not "preflight" (unless explaining the alias)
- [ ] "intent" not "transaction request"
- [ ] "policy engine" not "validation engine" or "rules engine"
- [ ] "block reason" not "error reason" or "rejection reason"
- [ ] "dashboard" not "admin panel" or "web UI" or "console"
- [ ] "reason field" not "justification" or "rationale"
- [ ] "non-custodial" not "self-hosted" or "keyless"
- [ ] "circuit breaker" not "kill switch" (unless in explanation context)

### 6. GEO / LLM Optimization
- [ ] Self-contained answer blocks (can be cited without surrounding context)
- [ ] Question-based H2/H3 headings that match developer search queries
- [ ] Specific numbers included where applicable

### 7. Navigation Consistency
- [ ] Page is listed in docs.json navigation
- [ ] Internal links point to valid pages (cross-reference with docs.json)

## Severity Levels

Each finding gets a severity:

| Severity | Meaning | Example |
|----------|---------|---------|
| **critical** | Breaks rendering or misleads readers | Missing frontmatter, wrong API endpoint |
| **high** | Violates core writing rules | Em dashes, filler words, wrong terminology |
| **medium** | Missing recommended structure | No Next Steps cards, fewer than 3 cross-links |
| **low** | Minor style or optimization issue | Paragraph slightly long, heading not question-form |

## Report Format (per page)

Each page gets a file at `/docs/tests/{section}-{page-name}.md`:

```markdown
# Test Report: {page title}

**File:** {path}
**Section:** {section name}
**Date:** {YYYY-MM-DD}
**Status:** PASS | FAIL | WARN

## Checklist Results

| Check | Result | Notes |
|-------|--------|-------|
| Frontmatter: title | PASS/FAIL | |
| Frontmatter: sidebarTitle | PASS/FAIL | |
| ... | | |

## Findings

### {severity}: {short description}
- **Line(s):** {line numbers}
- **Rule:** {which rule from WRITING-GUIDE.md}
- **Found:** {the problematic text}
- **Suggested fix:** {what it should be}

## Score

- Critical: {N}
- High: {N}
- Medium: {N}
- Low: {N}
- **Overall:** PASS (0 critical, 0 high) | WARN (has medium) | FAIL (has critical or high)
```

## How to Run

### Full validation (all pages)
```
/qa can you test and validate each page of documentation
```

### Single section
```
/qa validate the sdk section only
```

### Re-validate after fixes
```
/qa re-check pages that had FAIL status in /docs/tests/
```

## How to Write a Sub-Agent Prompt

Each sub-agent needs:

1. **The full validation checklist** (copy from above)
2. **The terminology table** from WRITING-GUIDE.md
3. **The list of pages to validate** (file paths)
4. **The output directory** (/docs/tests/)
5. **The report format** (template above)
6. **Clear instructions**: "Read each page. Check each rule. Write one report file per page."

### Example sub-agent prompt structure:

```
You are a documentation QA agent. Your job: validate {N} documentation pages
against the project's WRITING-GUIDE.md rules.

PAGES TO VALIDATE:
- /path/to/page1.mdx
- /path/to/page2.mdx

VALIDATION RULES:
{paste the checklist}

TERMINOLOGY TABLE:
{paste the table}

OUTPUT:
For each page, write a report to /docs/tests/{section}-{page-name}.md
using this format: {paste the template}

INSTRUCTIONS:
- Read each page fully
- Check every rule in the checklist
- Be specific: include line numbers and the exact problematic text
- Suggest concrete fixes, not vague advice
- A page PASSES only if it has 0 critical and 0 high findings
```

## Key Principles

1. **One agent per section, not per page.** Launching 80+ agents has diminishing
   returns. Section-level agents have context about related pages and can spot
   cross-referencing gaps.

2. **Checklist-driven, not vibes-based.** Every finding maps to a specific rule
   in WRITING-GUIDE.md. No subjective opinions.

3. **Severity matters.** Critical/high findings block a page from passing.
   Medium/low are improvement opportunities.

4. **Evidence-based.** Include line numbers and exact text. "Has filler words"
   is useless. "Line 47: 'simply call validate()' violates no-filler-words rule"
   is actionable.

5. **Parallel execution.** All section agents run simultaneously. The orchestrator
   waits for all to complete, then aggregates.

6. **Idempotent.** Running the same validation twice produces the same results
   (unless the docs changed). Reports overwrite, not append.
