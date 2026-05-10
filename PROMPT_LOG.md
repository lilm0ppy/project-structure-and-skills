# PROMPT_LOG

Purpose: keep a rolling, compressed summary of important prompts and why they matter.

Rules:
- Do not store full raw prompts unless they are short and highly important.
- Compress aggressively.
- Keep entries focused on future usefulness.

## Entry Template

### YYYY-MM-DD
- Prompt summary:
- Why it mattered:
- Agent action summary:
- Decisions made:
- Useful future context:
- Next prompt should remember:

---

### 2026-05-07
- Prompt summary: Build a reusable AI project-organization system in this repo, create the root control files, import current skills into `.claude/skills/` and `codex-friendly-skills/`, and avoid touching application/source code.
- Why it mattered: This defines the repo's operating model and future handoff/memory workflow.
- Agent action summary: Created the organization documents, mirrored the current skill libraries into the new structure, and rewrote `AGENTS.md` to align with the requested workflow.
- Decisions made:
  - Keep mirrored Claude and Codex skill folders separate
  - Use compressed state files rather than a monolithic instruction file
- Useful future context:
  - The original skill libraries still exist in their source folders
  - The mirrored project-structure folders should be treated as the active project-facing skill locations
- Next prompt should remember:
  - The next likely step is curating or creating project-specific skills inside this structure

### 2026-05-07
- Prompt summary: Audit the new project-organization system for gaps, duplication, context bloat, unclear instructions, and missing guidance for skills, handoffs, memory, and final response format.
- Why it mattered: This prompt shifts the repo from initial setup into maintainable operational quality.
- Agent action summary: Tightened ambiguous instructions, clarified which skill folders are active versus preserved, added file-update rules, and improved handoff and memory maintenance guidance.
- Decisions made:
  - Keep original skill folders as preserved sources and mirrored folders as the active working locations
  - Favor targeted clarifications over broad rewrites
- Useful future context:
  - The system now has clearer read-order and update-order guidance
  - The next meaningful improvement is curation, not more top-level documentation
- Next prompt should remember:
  - Focus on selecting a smaller default skill baseline and adding project-specific meta-skills
