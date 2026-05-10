# MEMORY

Purpose: durable, compressed memory for future agents.

Rules:
- Do not dump raw transcripts here.
- Only store compressed, durable context.
- Remove stale or duplicated memory when updating.
- If something is temporary, keep it in `PROJECT_STATE.md` or `TASK_LOG.md` instead.
- If a fact is uncertain, label it as uncertain rather than upgrading it into durable memory.

## Memory Update Procedure

When updating memory:
1. Keep only facts that are likely to matter across multiple future tasks.
2. Prefer merging with existing bullets instead of appending new near-duplicates.
3. Move short-lived execution detail to `PROJECT_STATE.md`, `TASK_LOG.md`, or `PROMPT_LOG.md`.
4. Remove stale memory when it would mislead a future agent.

## Core Project Goal

- Maintain a reusable AI project-organization system that can be dropped into new projects.
- Optimize token usage and context storage while improving agent output quality.
- Support Codex, Claude Code, and other coding agents with a shared operating model.

## Stable Concepts

- `AGENTS.md` defines how agents should work in this repo.
- `CONTEXT_INDEX.md` tells agents what context to read first.
- `PROJECT_STATE.md` is the current operational snapshot.
- `MEMORY.md` stores durable facts, not narratives.
- `HANDOFF.md` is the contract for cross-agent coordination.
- `SKILLS_INDEX.md` is the main catalog for deciding which skill to use.

## User Preferences

- Keep skills curated rather than loading everything blindly.
- Favor compressed, reusable documentation over long chat history.
- Preserve existing content and avoid destructive changes.
- Keep Codex-friendly and Claude-compatible skill systems separated but coordinated.

## Durable Repo Facts

- Claude-compatible skills are mirrored under `.claude/skills/`.
- Codex-friendly skills are mirrored under `codex-friendly-skills/`.
- The original imported skill libraries remain preserved in their existing source folders.

## Open Memory Hygiene Notes

- If future agents add repeated facts to logs and memory, compress them back down.
- Keep this file short enough that a future agent can read it in under a minute.
