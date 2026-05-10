# DECISIONS

Use this file for durable technical and workflow decisions only.

## Decision Template

### [DECISION-ID] Title
- Date:
- Status: Proposed | Accepted | Reversed | Deprecated
- Context:
- Decision:
- Alternatives considered:
- Tradeoffs:
- Follow-up:

---

### DEC-001 Universal project-organization files are first-class repo assets
- Date: 2026-05-07
- Status: Accepted
- Context: The repository is intended to be imported into new projects to improve agent behavior and context handling.
- Decision: Separate memory, state, prompt history, task history, handoffs, roadmap, and skill indexing into dedicated root files.
- Alternatives considered:
  - Keep all project guidance in a single large `AGENTS.md`
  - Store state only in chat history
- Tradeoffs:
  - More files to maintain
  - Much better scanability, lower context overhead, and cleaner handoffs
- Follow-up:
  - Maintain compression discipline so these files stay useful

### DEC-002 Keep Claude-compatible and Codex-friendly skills in separate project folders
- Date: 2026-05-07
- Status: Accepted
- Context: Different agents benefit from different assumptions and skill wording.
- Decision: Mirror skills into `.claude/skills/` and `codex-friendly-skills/` rather than mixing all skill formats in one place.
- Alternatives considered:
  - One shared folder for every skill
  - Rely only on external/global skill locations
- Tradeoffs:
  - Some duplication and sync overhead
  - Clearer targeting for different agent ecosystems
- Follow-up:
  - Consider a future sync or validation process
