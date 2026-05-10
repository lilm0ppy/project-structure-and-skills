# AGENTS

This repository is a universal AI project-organization system. Its job is to help Codex, Claude Code, and other coding agents preserve useful memory, reduce context bloat, coordinate handoffs, and use skills deliberately.

Do not treat this repo like an application codebase unless application code is later added. The default responsibility here is to maintain project-organization files, indexes, memory, handoffs, and curated skills.

## Operating Rules

- Do not modify application/source code unless the task explicitly requires it.
- Prefer updating the project-organization files in this repo over writing long free-form explanations in chat.
- Preserve meaningful existing content when updating files. Merge or append cleanly.
- Keep documentation compressed, durable, and easy for a future agent to scan quickly.
- Use only relevant skills. Do not load every skill automatically.
- Prefer project-specific skills over generic skills when both exist.
- Treat `Original Claude code skills/` and `Original Codex skills/` as preserved source libraries, not the default working locations.
- Treat `.claude/skills/` and `codex-friendly-skills/` as the active project-facing skill locations.

## Before Major Work

Before major work:
1. Read `CONTEXT_INDEX.md`.
2. Read `PROJECT_STATE.md`.
3. Read `HANDOFF.md` if an active handoff exists.
4. Read relevant skills from `.claude/skills/` or `codex-friendly-skills/`.
5. Inspect relevant source files before proposing changes.
6. Make a plan before editing if the task is complex.
7. Make the smallest safe change.
8. Run tests/checks where practical.
9. Update `TASK_LOG.md` after meaningful work.
10. Update `PROJECT_STATE.md` if the repo state changed.
11. Update `DECISIONS.md` only if a real technical decision was made.
12. Add compressed entries to `PROMPT_LOG.md` for important prompts.
13. Keep `MEMORY.md` compressed and durable.
14. End with files changed, tests run, assumptions, risks, and next step.

## Context Discipline

To avoid context bloat:
- Read indexes and state files first, not every historical log.
- Pull in only the skill files that match the task.
- Prefer summaries over transcripts.
- Update memory with durable facts, not narration.
- If a log entry is obsolete or duplicated elsewhere, summarize it instead of repeating it.
- If uncertain, mark information as uncertain instead of pretending it is fact.

## Memory Rules

- Do not dump raw chat logs into memory.
- Prefer compressed summaries.
- Preserve decisions, constraints, current state, and next actions.
- Remove outdated memory when it becomes misleading.
- Keep `MEMORY.md` focused on durable context that still matters after the current task ends.

## Skill Rules

- Use only relevant skills.
- Do not load every skill automatically.
- For Codex, read relevant `SKILL.md` files manually when needed.
- For Claude Code, project skills can live in `.claude/skills/`.
- Prefer project-specific skills over generic skills when both exist.
- Use `SKILLS_INDEX.md` to decide what skill fits the task.
- Read at most the smallest useful skill set first, then expand only if the task still needs more guidance.

## Preferred Baseline Policy

This repo has a curated default skill baseline for both Codex and Claude Code.

- Do not load all preferred skills automatically.
- Choose only the smallest relevant subset for the current task.
- Start with one primary skill, then add one or two supporting skills only if they reduce risk or ambiguity.
- If a preferred skill is missing, note that a placeholder or new skill is needed instead of pretending it exists.

Practical selection pattern:
- Planning or decomposition: use `deep-planner` for complex planning before implementation.
- Implementation: use one primary domain skill plus only the supporting skills that are actually needed.
- Debugging: start with `debugging-wizard`, then add testing or monitoring skills if the evidence points there.
- Review: use `handoff-reviewer` when reviewing another agent's work, and add `code-reviewer` or `test-master` when risk is non-trivial.
- Memory and logs: use `context-compressor` when updating memory/log files.
- Handoffs: use `handoff-writer` when creating Claude <-> Codex handoffs.
- Project-state maintenance: use `project-memory-updater` after meaningful project changes.
- Prompt compression: use `prompt-log-compressor` after important prompts or planning sessions.

### Agent-specific skill usage

- Codex: prefer `codex-friendly-skills/`; consult original/source skill folders only when auditing or syncing the mirrors.
- Claude Code: prefer `.claude/skills/`; use `codex-friendly-skills/` only when comparing formats or porting skills.
- Any agent: do not read both mirrored and original skill trees for the same task unless the task is specifically about skill maintenance.
- Both agents: use the same curated baseline policy, but read from their own active skill folder first.

## Handoff Rules

- Claude can create plans and write `HANDOFF.md` for Codex.
- Codex can implement and update `HANDOFF.md` for Claude review.
- Review agents should check whether implementation followed the plan.
- Every handoff should include acceptance criteria and risks.
- Use the templates in `HANDOFF.md` instead of inventing new handoff formats.
- When a handoff becomes stale or completed, replace it with a compressed updated handoff or mark it closed instead of letting multiple active handoffs pile up.

## Files to Use

Core control files:
- `CONTEXT_INDEX.md`: first stop for deciding what context matters
- `PROJECT_STATE.md`: current state snapshot
- `MEMORY.md`: durable compressed memory
- `DECISIONS.md`: technical decision log
- `TASK_LOG.md`: execution history
- `PROMPT_LOG.md`: compressed prompt history
- `HANDOFF.md`: structured handoff system
- `ROADMAP.md`: milestone and backlog view
- `SKILLS_INDEX.md`: skill catalog and selection guide

Skill locations:
- `.claude/skills/`: Claude-compatible project skills
- `codex-friendly-skills/`: agent-neutral skills with Codex usage guidance
- `Original Claude code skills/`: preserved source library
- `Original Codex skills/`: preserved source library

## Update Rules By File

- Update `PROJECT_STATE.md` when the current goal, active task, known risks, or next best step changes.
- Update `MEMORY.md` only for durable facts that should survive across many future tasks.
- Update `DECISIONS.md` only for real decisions with alternatives or tradeoffs.
- Update `TASK_LOG.md` after meaningful implementation, audit, planning, or organizational work.
- Update `PROMPT_LOG.md` only for prompts that change future behavior or preserve reusable context.
- Update `HANDOFF.md` whenever work is being transferred, paused, or split between roles.

## Final Response Format

Every substantial response should end with:
- Summary
- Files changed
- Tests/checks run
- Skills used
- Assumptions
- Risks / unresolved issues
- Suggested next step

## Current Repo-Specific Note

This repo already contains imported skill libraries. Treat them as curated resources, not as files to casually rewrite during unrelated tasks.
