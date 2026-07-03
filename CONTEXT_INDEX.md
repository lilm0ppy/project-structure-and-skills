# CONTEXT_INDEX

This is the first file agents should use to decide what context matters.

## Always read first

- `AGENTS.md`
- `PROJECT_STATE.md`
- `HANDOFF.md` if there is an active task
- Then stop and decide what additional context is actually necessary before reading more files.

## For planning

- `MEMORY.md`
- `PROJECT_STATE.md`
- `DECISIONS.md`
- `ROADMAP.md`
- `SKILLS_INDEX.md`
- relevant planning skills

## For coding

- `AGENTS.md`
- `PROJECT_STATE.md`
- `HANDOFF.md`
- relevant skill files
- relevant source files

## For OTAInspectionApp mapping

- `OTAInspectionApp-Map/README.md`
- `OTAInspectionApp-Map/APP_CONTEXT.md`
- `OTAInspectionApp-Map/ARCHITECTURE_AND_DATA_FLOW.md`
- `OTAInspectionApp-Map/PROJECT_STATE.md`
- `OTAInspectionApp-Map/DECISIONS_AND_OPEN_QUESTIONS.md`
- Read this map pack before making deep app changes so you do not rely on stale app-local handoff docs alone.

Default skill path selection:
- Codex: `codex-friendly-skills/`
- Claude Code: `.claude/skills/`
- Use `Original Claude code skills/` or `Original Codex skills/` only for audits, migration work, or mirror maintenance

## For debugging

- `TASK_LOG.md`
- `PROJECT_STATE.md`
- `HANDOFF.md`
- `debugging-wizard` skill
- `test-master` skill

## For review

- `HANDOFF.md`
- `TASK_LOG.md`
- `DECISIONS.md`
- `code-reviewer` skill
- `test-master` skill

## For memory updates

- `MEMORY.md`
- `PROJECT_STATE.md`
- `DECISIONS.md`
- `PROMPT_LOG.md`
- `TASK_LOG.md`
- `context-compressor` skill if available

## What not to read unless needed

- Old `TASK_LOG.md` entries that predate the current problem and do not touch the same area
- Old `PROMPT_LOG.md` entries that were purely tactical and produced no durable decision
- Skill folders unrelated to the task domain
- Large historical handoff sections once a newer handoff supersedes them
- Entire mirrored skill trees when only one or two skills are relevant
- Original source skill folders during routine task work

## How to avoid context bloat

- Start with indexes and state files, not raw history.
- Pull in logs only when current behavior, decisions, or failures depend on them.
- Read one or two relevant skills, not the whole library.
- Summarize findings back into the project files rather than preserving long chat artifacts.
- Prefer updating one authoritative file instead of repeating the same fact across many files.

## How to decide whether an old log entry matters

An old entry matters if it:
- explains the current architecture or constraint
- records a still-active decision
- describes a recurring bug or known risk
- documents why a tempting path was rejected

An old entry usually does not matter if it:
- describes a one-off action with no lasting consequence
- repeats facts already preserved in `MEMORY.md` or `PROJECT_STATE.md`
- belongs to an abandoned direction with no current relevance
