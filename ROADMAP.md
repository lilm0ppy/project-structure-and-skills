# ROADMAP

Use this as the practical milestone tracker for the repository.

## Current Milestone

- Establish the reusable project-organization system and mirror the current skill libraries into project-facing folders.

## Next 3-5 Milestones

1. Curate the default project skill set and identify which imported skills are part of the standard baseline.
2. Create the first project-specific meta-skills such as `context-compressor`, `handoff-writer`, and `project-memory-updater`.
3. Define a lightweight maintenance workflow for keeping mirrored skill folders in sync with source skill libraries.
4. Add example handoff and memory-update flows so future agents can follow a concrete pattern.
5. Optionally package this structure as a reusable starter kit for other repos.

## Backlog

- Decide whether mirrored skills should be manually curated or auto-synced.
- Add a validation checklist for updating project-organization files.
- Create sample project templates that consume this system.
- Add optional domain packs for data science, trading, bots, and web apps.

## Parking Lot

- Hook-based automation for keeping logs and memory fresh
- Automatic stale-memory detection
- Repo bootstrap scripts for importing this structure elsewhere

## Blockers

- None recorded yet.

## Open Questions

- Which imported skills belong in the default project baseline versus optional add-ons?
- Should project-specific meta-skills live in both Claude and Codex folders or only in agent-neutral form?
- Is a sync process worth the maintenance overhead for mirrored skill libraries?

## Completed Milestones

- Imported current skill libraries into project-facing Claude and Codex skill folders.
- Created the core project-organization files and context system.
