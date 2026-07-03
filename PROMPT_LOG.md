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

### 2026-06-24
- Prompt summary: Read the project-structure folder, deeply analyze `OTAInspectionApp/`, apply relevant skills, and produce only clean markdown docs that map the app's context, design, data flow, project state, and open decisions without changing application code.
- Why it mattered: This is the first app-specific analysis pack meant to reduce future implementation risk and avoid relying on stale handoff notes alone.
- Agent action summary: Audited the live app workspace, ran tests/types/Expo doctor, compared code against app-local docs, and created a dedicated `OTAInspectionApp-Map/` documentation pack inside `Project Structure/`.
- Decisions made:
  - Preserve the meta-repo docs and add a dedicated app-map pack instead of rewriting the project-system roadmap/state files into app-specific content
  - Treat runtime code and tests as the strongest source of truth when app-local docs disagree
- Useful future context:
  - The current app has evolved far beyond the original AsyncStorage-only spec
  - The biggest current drift is between older "encrypted SQLCipher runtime" documentation and the present `data/database.ts` behavior, which migrates to plain SQLite for normal runtime use
  - `app.json` currently sets `android.allowBackup: true`, which may conflict with older hardening assumptions
- Next prompt should remember:
  - Read `OTAInspectionApp-Map/README.md` before planning app changes and resolve the owner questions in `DECISIONS_AND_OPEN_QUESTIONS.md` before major architecture work
