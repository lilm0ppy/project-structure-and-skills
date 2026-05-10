---
name: javascript-pro
description: Writes, debugs, and refactors JavaScript code using modern ES2023+ features, async/await patterns, ESM module systems, and Node.js APIs. Use when building vanilla JavaScript applications, implementing Promise-based async flows, optimising browser or Node.js performance, working with Web Workers or Fetch API, or reviewing .js/.mjs/.cjs files for correctness and best practices.
license: MIT
metadata:
  author: https://github.com/Jeffallan
  version: "1.1.0"
  domain: language
  triggers: JavaScript, ES2023, async await, Node.js, vanilla JavaScript, Web Workers, Fetch API, browser API, module system
  role: specialist
  scope: implementation
  output-format: code
  related-skills: fullstack-guardian
---

# JavaScript Pro

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
- Building vanilla JavaScript applications
- Implementing async/await patterns and Promise handling
- Working with modern module systems (ESM/CJS)
- Optimizing browser performance and memory usage
- Developing Node.js backend services
- Implementing Web Workers, Service Workers, or browser APIs

Do not use this skill when:
- The task is unrelated to this skill's domain
- A simpler general coding response is enough
- The skill would add unnecessary process or context bloat

## When to Use This Skill

- Building vanilla JavaScript applications
- Implementing async/await patterns and Promise handling
- Working with modern module systems (ESM/CJS)
- Optimizing browser performance and memory usage
- Developing Node.js backend services
- Implementing Web Workers, Service Workers, or browser APIs

## Core Workflow

1. **Analyze requirements** â€” Review `package.json`, module system, Node version, browser targets; confirm `.js`/`.mjs`/`.cjs` conventions
2. **Design architecture** â€” Plan modules, async flows, and error handling strategies
3. **Implement** â€” Write ES2023+ code with proper patterns and optimisations
4. **Validate** â€” Run linter (`eslint --fix`); if linter fails, fix all reported issues and re-run before proceeding. Check for memory leaks with DevTools or `--inspect`, verify bundle size; if leaks are found, resolve them before continuing
5. **Test** â€” Write comprehensive tests with Jest achieving 85%+ coverage; if coverage falls short, add missing cases and re-run. Confirm no unhandled Promise rejections

## Reference Guide

Load detailed guidance based on context:

| Topic | Reference | Load When |
|-------|-----------|-----------|
| Modern Syntax | `references/modern-syntax.md` | ES2023+ features, optional chaining, private fields |
| Async Patterns | `references/async-patterns.md` | Promises, async/await, error handling, event loop |
| Modules | `references/modules.md` | ESM vs CJS, dynamic imports, package.json exports |
| Browser APIs | `references/browser-apis.md` | Fetch, Web Workers, Storage, IntersectionObserver |
| Node Essentials | `references/node-essentials.md` | fs/promises, streams, EventEmitter, worker threads |

## Constraints

### MUST DO
- Use ES2023+ features exclusively
- Use `X | null` or `X | undefined` patterns
- Use optional chaining (`?.`) and nullish coalescing (`??`)
- Use async/await for all asynchronous operations
- Use ESM (`import`/`export`) for new projects
- Implement proper error handling with try/catch
- Add JSDoc comments for complex functions
- Follow functional programming principles

### MUST NOT DO
- Use `var` (always use `const` or `let`)
- Use callback-based patterns (prefer Promises)
- Mix CommonJS and ESM in the same module
- Ignore memory leaks or performance issues
- Skip error handling in async functions
- Use synchronous I/O in Node.js
- Mutate function parameters
- Create blocking operations in the browser

## Key Patterns with Examples

### Async/Await Error Handling
```js
// âœ… Correct â€” always handle async errors explicitly
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return await response.json();
  } catch (err) {
    console.error("fetchUser failed:", err);
    return null;
  }
}

// âŒ Incorrect â€” unhandled rejection, no null guard
async function fetchUser(id) {
  const response = await fetch(`/api/users/${id}`);
  return response.json();
}
```

### Optional Chaining & Nullish Coalescing
```js
// âœ… Correct
const city = user?.address?.city ?? "Unknown";

// âŒ Incorrect â€” throws if address is undefined
const city = user.address.city || "Unknown";
```

### ESM Module Structure
```js
// âœ… Correct â€” named exports, no default-only exports for libraries
// utils/math.mjs
export const add = (a, b) => a + b;
export const multiply = (a, b) => a * b;

// consumer.mjs
import { add } from "./utils/math.mjs";

// âŒ Incorrect â€” mixing require() with ESM
const { add } = require("./utils/math.mjs");
```

### Avoid var / Prefer const
```js
// âœ… Correct
const MAX_RETRIES = 3;
let attempts = 0;

// âŒ Incorrect
var MAX_RETRIES = 3;
var attempts = 0;
```

## Output Templates

When implementing JavaScript features, provide:
1. Module file with clean exports
2. Test file with comprehensive coverage
3. JSDoc documentation for public APIs
4. Brief explanation of patterns used

## Validation Checklist

Before finishing:
- [ ] Relevant files were inspected
- [ ] Changes follow the project conventions
- [ ] Tests or checks were run where practical
- [ ] Edge cases were considered
- [ ] Final response includes files changed, checks run, assumptions, and risks

