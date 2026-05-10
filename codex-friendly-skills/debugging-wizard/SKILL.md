---
name: debugging-wizard
description: Parses error messages, traces execution flow through stack traces, correlates log entries to identify failure points, and applies systematic hypothesis-driven methodology to isolate and resolve bugs. Use when investigating errors, analyzing stack traces, finding root causes of unexpected behavior, troubleshooting crashes, or performing log analysis, error investigation, or root cause analysis.
license: MIT
metadata:
  author: https://github.com/Jeffallan
  version: "1.1.0"
  domain: quality
  triggers: debug, error, bug, exception, traceback, stack trace, troubleshoot, not working, crash, fix issue
  role: specialist
  scope: analysis
  output-format: analysis
  related-skills: test-master, fullstack-guardian, monitoring-expert
---

# Debugging Wizard

## Codex Usage

When using this skill in Codex:
1. Read this SKILL.md before starting the task.
2. Read AGENTS.md if it exists.
3. Inspect relevant project files before editing.
4. Make the smallest safe change that satisfies the task.
5. Prefer explicit, testable changes over broad rewrites.
6. Run relevant tests, linters, type checks, or explain why they were not run.
7. End with:
   - Files changed
   - Tests/checks run
   - Assumptions
   - Remaining risks
   - Suggested next step

## Trigger Guidance

Use this skill when the task involves:
- debug
- error
- bug
- exception
- traceback
- stack trace

Do not use this skill when:
- The task is unrelated to this skill's domain
- A simpler general coding response is enough
- The skill would add unnecessary process or context bloat

Expert debugger applying systematic methodology to isolate and resolve issues in any codebase.

## Core Workflow

1. **Reproduce** - Establish consistent reproduction steps
2. **Isolate** - Narrow down to smallest failing case
3. **Hypothesize and test** - Form testable theories, verify/disprove each one
4. **Fix** - Implement and verify solution
5. **Prevent** - Add tests/safeguards against regression

## Reference Guide

Load detailed guidance based on context:

<!-- Systematic Debugging row adapted from obra/superpowers by Jesse Vincent (@obra), MIT License -->

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Debugging Tools | `references/debugging-tools.md` | Setting up debuggers by language |
| Common Patterns | `references/common-patterns.md` | Recognizing bug patterns |
| Strategies | `references/strategies.md` | Binary search, git bisect, time travel |
| Quick Fixes | `references/quick-fixes.md` | Common error solutions |
| Systematic Debugging | `references/systematic-debugging.md` | Complex bugs, multiple failed fixes, root cause analysis |

## Constraints

### MUST DO
- Reproduce the issue first
- Gather complete error messages and stack traces
- Test one hypothesis at a time
- Document findings for future reference
- Add regression tests after fixing
- Remove all debug code before committing

### MUST NOT DO
- Guess without testing
- Make multiple changes at once
- Skip reproduction steps
- Assume you know the cause
- Debug in production without safeguards
- Leave console.log/debugger statements in code

## Common Debugging Commands

**Python (pdb)**
```bash
python -m pdb script.py          # launch debugger
# inside pdb:
# b 42          â€” set breakpoint at line 42
# n             â€” step over
# s             â€” step into
# p some_var    â€” print variable
# bt            â€” print full traceback
```

**JavaScript (Node.js)**
```bash
node --inspect-brk script.js     # pause at first line, attach Chrome DevTools
# In Chrome: open chrome://inspect â†’ click "inspect"
# Sources panel: add breakpoints, watch expressions, step through
```

**Git bisect (regression hunting)**
```bash
git bisect start
git bisect bad                   # current commit is broken
git bisect good v1.2.0           # last known good tag/commit
# Git checks out midpoint â€” test, then:
git bisect good   # or: git bisect bad
# Repeat until git identifies the first bad commit
git bisect reset
```

**Go (delve)**
```bash
dlv debug ./cmd/server           # build & attach
# (dlv) break main.go:55
# (dlv) continue
# (dlv) print myVar
```

## Output Templates

When debugging, provide:
1. **Root Cause**: What specifically caused the issue
2. **Evidence**: Stack trace, logs, or test that proves it
3. **Fix**: Code change that resolves it
4. **Prevention**: Test or safeguard to prevent recurrence

## Validation Checklist

Before finishing:
- [ ] Relevant files were inspected
- [ ] Changes follow the project conventions
- [ ] Tests or checks were run where practical
- [ ] Edge cases were considered
- [ ] Final response includes files changed, checks run, assumptions, and risks

