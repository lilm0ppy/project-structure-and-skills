# PROJECT_STATE

## Current Project Goal

Build and maintain a universal AI project-organization system that can be imported at the start of new projects to improve agent coordination, memory durability, skill usage, and context efficiency.

## Current Architecture

- Root control docs define how agents work, preserve state, and coordinate handoffs.
- `.claude/skills/` contains Claude-compatible project skills.
- `codex-friendly-skills/` contains agent-neutral or Codex-oriented skills.
- Historical execution, prompts, decisions, and roadmap items are separated into dedicated files to avoid mixing concerns.

## Important Folders and Files

- `AGENTS.md`: master repo instructions for agents
- `CONTEXT_INDEX.md`: what to read first, and when
- `MEMORY.md`: durable compressed memory
- `PROJECT_STATE.md`: current status snapshot
- `DECISIONS.md`: decision log
- `TASK_LOG.md`: execution history
- `PROMPT_LOG.md`: compressed prompt history
- `HANDOFF.md`: handoff templates
- `ROADMAP.md`: milestones and backlog
- `SKILLS_INDEX.md`: skill catalog and usage guidance
- `.claude/skills/`: Claude-compatible skills
- `codex-friendly-skills/`: Codex-friendly skills

## Working Features

- Core project-organization document set exists.
- Existing Claude and Codex skill libraries have been imported into the new structure without modifying the originals.
- AGENT guidance now points agents toward selective skill loading and compressed state management.
- Preserved source skill folders are separated from the active project-facing skill folders.
- A curated preferred skill baseline is now defined for planning, coding, data/modelling, web/API work, safety/reliability, and memory/handoff maintenance.

## Broken or Incomplete Features

- No custom project-specific meta-skills have been created yet.
- No automated sync process exists yet between source skill folders and mirrored project-structure folders.
- Handoff, memory, and log files are templates plus initial state; they need to be maintained as work continues.
- Several preferred baseline skills are still missing and need placeholders or real implementations.

## Current Active Task

Maintain a Claude Code and Codex compatible project-organization system with a curated default skill baseline and explicit selective-skill-loading policy.

## Current Preferred Skill Policy

Agents should not load the whole preferred baseline automatically. They should choose only the smallest relevant subset for the task.

Preferred default baseline:
- Core coding / repo work: `deep-planner`, `architecture-designer`, `python-pro`, `debugging-wizard`, `test-master`, `code-reviewer`
- Data / modelling: `pandas-pro`, `sql-pro`, `ml-pipeline`, `feature-engineering-reviewer`, `backtest-sanity-checker`
- Web / APIs / bots: `api-designer`, `fastapi-expert`, `typescript-pro`, `react-expert`, `nextjs-developer`, `notification-bot-builder`
- Safety / reliability: `secure-code-guardian`, `monitoring-expert`, `devops-engineer`
- Context / memory / handoff: `context-compressor`, `handoff-writer`, `handoff-reviewer`, `project-memory-updater`, `prompt-log-compressor`

## Known Risks

- Mirrored skill folders can drift from the original source folders if updated manually in only one place.
- Agents may still over-read logs unless `CONTEXT_INDEX.md` is followed consistently.
- If logs are not compressed periodically, this system can recreate the same context bloat it is meant to prevent.

## Next Best Step

Create placeholder or real skill folders for the missing preferred baseline skills, starting with `deep-planner`, `context-compressor`, `handoff-writer`, `handoff-reviewer`, and `project-memory-updater`.
