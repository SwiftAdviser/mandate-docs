# QA Report: cli/login.mdx

## Checklist

| # | Rule | Pass? |
|---|------|:-----:|
| 1 | Frontmatter: title, sidebarTitle, description | PASS |
| 2 | No em dashes (U+2014) | PASS |
| 3 | No filler words | PASS |
| 4 | Short paragraphs (2-4 sentences) | PASS |
| 5 | "Next Steps" CardGroup at bottom | PASS |
| 6 | 3-5 cross-links | PASS (3 cards + 1 inline link to /dashboard/overview) |
| 7 | Correct terminology | PASS ("runtime key" used throughout) |
| 8 | CLI-specific: commands, flags, examples, output, prerequisites | PASS |

## Findings

- **Line 9**: Clear opening. "You run this once per agent." sets the right expectation.
- **Line 17-24**: Options table is complete. Short aliases shown for `-p` and `-d`.
- **Line 38-45**: Output block shows realistic JSON. Runtime key is masked with `...xyz` suffix, matching the "masked in output" note on line 47.
- **Line 49-51**: "What is the claim URL?" section is self-contained. Good for LLM citation. The inline link to `/dashboard/overview` counts toward cross-links.
- **Line 53-55**: Note callout about zero address is clear. Tells you exactly what to do: call `activate`.
- **Line 59**: Credential file details are useful but partially duplicate the overview page's credential storage section. Not a problem for standalone reading.

## Developer Experience Notes

- **Flow is clear**: login -> get key -> optionally activate. The page tells me what happens, what I get back, and what to do next.
- **Claim URL explanation**: Essential for onboarding. Without this, a developer would wonder what to do with the URL in the output.
- **Missing**: No error output example. What happens if I run `login` when credentials already exist? Does it overwrite? Warn? Fail? Line 59 says "delete the file and run login again" but does not say what happens if I forget to delete.
- **Missing**: No mention of `MANDATE_RUNTIME_KEY` environment variable as an alternative to the credentials file. If the SDK supports env vars, the CLI page should mention it.

## Score

**9/10**

Solid reference page. Missing error scenarios (duplicate login, invalid flags) would round it out.
