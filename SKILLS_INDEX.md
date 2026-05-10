# SKILLS_INDEX

Use this file to decide which skills matter before major work. Prefer the smallest relevant set.

Legend:
- Where it should live: `.claude/skills/`, `codex-friendly-skills/`, or both
- Status: Essential | Optional | Project-specific

Selection rules:
- Choose one primary domain skill first.
- Add supporting skills only when they clearly reduce risk or ambiguity.
- Prefer mirrored project-facing skill folders over original source folders.
- If a task is simple, a general coding response may be better than loading any skill.
- Do not load the entire preferred baseline automatically.

## Curated Default Baseline

This is the preferred default baseline for the project system. It is shared across Codex and Claude Code, but each agent should read from its own active skill folder first.

### Core coding / repo work

#### deep-planner
- Purpose: Deep planning for complex implementation work before coding starts.
- When to use: Multi-step features, unclear requirements, risky refactors, or work that needs a deliberate implementation plan.
- Status: Missing / placeholder needed
- Notes: Preferred default. Should be the first planning skill for complex work.

#### architecture-designer
- Purpose: System design, ADRs, tradeoff analysis, and architecture planning.
- When to use: Major refactors, new systems, scaling questions, or structural design decisions.
- Status: Preferred default
- Notes: Use with `deep-planner` for complex planning, not for every small task.

#### python-pro
- Purpose: Python implementation with typing, async patterns, testing, and validation habits.
- When to use: Python features, refactors, scripts, services, utilities, and production-grade backend logic.
- Status: Preferred default
- Notes: Primary Python implementation skill.

#### debugging-wizard
- Purpose: Systematic debugging and root-cause analysis.
- When to use: Broken tests, runtime errors, unclear repo behavior, tracebacks, or log-driven investigations.
- Status: Preferred default
- Notes: Start here for diagnosis before adding more specialized support skills.

#### test-master
- Purpose: Test planning and implementation across unit, integration, regression, performance, and security.
- When to use: Adding tests, analyzing coverage, stabilizing flaky behavior, or designing validation strategy.
- Status: Preferred default
- Notes: Primary validation support skill.

#### code-reviewer
- Purpose: Broad code review for correctness, maintainability, security, and quality risks.
- When to use: Before merging risky changes, during audits, or when validating a substantial implementation.
- Status: Preferred default
- Notes: Use for final review passes or high-risk work.

### Data / modelling

#### pandas-pro
- Purpose: DataFrame manipulation, cleaning, joins, aggregation, and pandas performance work.
- When to use: CSV/parquet work, feature tables, exploratory data processing, and tabular transformations.
- Status: Preferred default
- Notes: Primary tabular-data skill.

#### sql-pro
- Purpose: SQL query design, schema modelling, indexing, and query-plan analysis.
- When to use: Database-heavy tasks, migrations, analytics queries, performance tuning, and schema design.
- Status: Preferred default
- Notes: Pair with `pandas-pro` or `ml-pipeline` when data flows cross storage and processing layers.

#### ml-pipeline
- Purpose: Model training, evaluation, orchestration, feature pipelines, and MLOps structure.
- When to use: ML workflows, experiment tracking, retraining flows, and feature engineering pipelines.
- Status: Preferred default
- Notes: Use for end-to-end modelling and pipeline structure.

#### feature-engineering-reviewer
- Purpose: Review tabular and ML feature engineering for leakage, stability, and usefulness.
- When to use: Before locking feature pipelines or reviewing model-input changes.
- Status: Missing / placeholder needed
- Notes: Preferred default for modelling review work.

#### backtest-sanity-checker
- Purpose: Catch invalid assumptions, leakage, lookahead bias, and evaluation mistakes in backtests.
- When to use: Backtesting, research validation, or strategy review.
- Status: Missing / placeholder needed
- Notes: Preferred default for research and evaluation sanity checks.

### Web / APIs / bots

#### api-designer
- Purpose: API contracts, schemas, pagination, versioning, and interface design.
- When to use: REST or GraphQL planning, endpoint contracts, or API surface cleanup.
- Status: Preferred default
- Notes: Use before implementation when API design choices matter.

#### fastapi-expert
- Purpose: FastAPI-specific implementation patterns.
- When to use: Python API backend work using FastAPI, Pydantic, auth flows, or async SQLAlchemy.
- Status: Preferred default
- Notes: Primary Python API framework skill.

#### typescript-pro
- Purpose: TypeScript architecture, advanced types, and type-safety patterns.
- When to use: TypeScript-heavy application code, typed APIs, or tsconfig/type-system work.
- Status: Preferred default
- Notes: Primary TypeScript implementation skill.

#### react-expert
- Purpose: React components, hooks, rendering, state management, and performance.
- When to use: React UI work, component refactors, state bugs, or performance issues.
- Status: Preferred default
- Notes: Use for React-specific implementation and review.

#### nextjs-developer
- Purpose: Next.js full-stack and App Router patterns.
- When to use: Next.js pages, routing, metadata, server components, server actions, and deployment-oriented work.
- Status: Preferred default
- Notes: Use instead of generic React-only guidance when the repo is clearly Next.js.

#### notification-bot-builder
- Purpose: Build bots for alerts, reports, and notifications.
- When to use: Monitoring bots, scheduled digests, webhook-based messaging, or operations automations.
- Status: Missing / placeholder needed
- Notes: Preferred default for bot-oriented workflow automation.

### Safety / reliability

#### secure-code-guardian
- Purpose: Secure coding, auth, authorization, secrets handling, and OWASP-style hardening.
- When to use: Security-sensitive features, user data, API keys, auth flows, or payment-adjacent work.
- Status: Preferred default
- Notes: Add when risk touches user data, trust boundaries, or sensitive integrations.

#### monitoring-expert
- Purpose: Observability, logging, metrics, tracing, dashboards, alerts, and production diagnostics.
- When to use: Reliability work, incidents, health checks, bot monitoring, or instrumentation.
- Status: Preferred default
- Notes: Primary operational-observability skill.

#### devops-engineer
- Purpose: CI/CD, Docker, infrastructure as code, deployment flows, and platform operations.
- When to use: GitHub Actions, containerization, deployment pipelines, environments, and release automation.
- Status: Preferred default
- Notes: Add when deployment or runtime environment work is involved.

### Context / memory / handoff

#### context-compressor
- Purpose: Compress logs, memory, state, and notes into durable low-noise summaries.
- When to use: Updating `MEMORY.md`, `TASK_LOG.md`, `PROMPT_LOG.md`, or cleaning bloated context files.
- Status: Missing / placeholder needed
- Notes: Preferred default for memory/log maintenance.

#### handoff-writer
- Purpose: Turn current work into a clean handoff packet.
- When to use: Before pausing, switching agents, or splitting planning from implementation.
- Status: Missing / placeholder needed
- Notes: Preferred default for Claude <-> Codex handoffs.

#### handoff-reviewer
- Purpose: Validate whether a handoff or another agent's work is complete and actionable.
- When to use: Before accepting a handoff, after implementation, or when reviewing another agent's work.
- Status: Missing / placeholder needed
- Notes: Preferred default for reviewer workflows.

#### project-memory-updater
- Purpose: Update `MEMORY.md`, `PROJECT_STATE.md`, and related files without adding noise.
- When to use: After major milestones or whenever durable context changed.
- Status: Missing / placeholder needed
- Notes: Preferred default after meaningful project changes.

#### prompt-log-compressor
- Purpose: Summarize important prompts and preserve only future-useful context.
- When to use: After long strategy threads, large planning sessions, or repeated user corrections.
- Status: Missing / placeholder needed
- Notes: Preferred default after important prompts or planning sessions.

## Core modelling/data skills

### python-pro
- Purpose: Python implementation with typing, async patterns, testing, and validation habits.
- When to use: Python features, refactors, scripts, services, utilities, and production-grade backend logic.
- Where it should live: both
- Status: Essential

### pandas-pro
- Purpose: DataFrame manipulation, cleaning, joins, aggregation, and pandas performance work.
- When to use: CSV/parquet work, feature tables, exploratory data processing, and tabular transformations.
- Where it should live: both
- Status: Essential

### sql-pro
- Purpose: SQL query design, schema modelling, indexing, and query-plan analysis.
- When to use: Database-heavy tasks, migrations, analytics queries, performance tuning, and schema design.
- Where it should live: both
- Status: Essential

### ml-pipeline
- Purpose: Model training, evaluation, orchestration, feature pipelines, and MLOps structure.
- When to use: ML workflows, experiment tracking, retraining flows, and feature engineering pipelines.
- Where it should live: both
- Status: Essential

### debugging-wizard
- Purpose: Systematic debugging and root-cause analysis.
- When to use: Broken tests, runtime errors, unclear repo behavior, tracebacks, or log-driven investigations.
- Where it should live: both
- Status: Essential

### test-master
- Purpose: Test planning and implementation across unit, integration, regression, performance, and security.
- When to use: Adding tests, analyzing coverage, stabilizing flaky behavior, or designing validation strategy.
- Where it should live: both
- Status: Essential

### code-reviewer
- Purpose: Broad code review for correctness, maintainability, security, and quality risks.
- When to use: Before merging risky changes, during audits, or when validating a substantial implementation.
- Where it should live: both
- Status: Essential

### architecture-designer
- Purpose: System design, ADRs, tradeoff analysis, and architecture planning.
- When to use: Major refactors, new systems, scaling questions, or structural design decisions.
- Where it should live: both
- Status: Essential

## Web/API/bot skills

### api-designer
- Purpose: API contracts, schemas, pagination, versioning, and interface design.
- When to use: REST or GraphQL planning, endpoint contracts, or API surface cleanup.
- Where it should live: both
- Status: Essential

### fastapi-expert
- Purpose: FastAPI-specific implementation patterns.
- When to use: Python API backend work using FastAPI, Pydantic, auth flows, or async SQLAlchemy.
- Where it should live: both
- Status: Essential

### typescript-pro
- Purpose: TypeScript architecture, advanced types, and type-safety patterns.
- When to use: TypeScript-heavy application code, typed APIs, or tsconfig/type-system work.
- Where it should live: both
- Status: Essential

### javascript-pro
- Purpose: Modern JavaScript implementation and debugging.
- When to use: Node.js scripts, browser logic, async flows, or plain JS application code.
- Where it should live: both
- Status: Essential

### react-expert
- Purpose: React components, hooks, rendering, state management, and performance.
- When to use: React UI work, component refactors, state bugs, or performance issues.
- Where it should live: both
- Status: Essential

### nextjs-developer
- Purpose: Next.js full-stack and App Router patterns.
- When to use: Next.js pages, routing, metadata, server components, server actions, and deployment-oriented work.
- Where it should live: both
- Status: Essential

### devops-engineer
- Purpose: CI/CD, Docker, infrastructure as code, deployment flows, and platform operations.
- When to use: GitHub Actions, containerization, deployment pipelines, environments, and release automation.
- Where it should live: both
- Status: Essential

### monitoring-expert
- Purpose: Observability, logging, metrics, tracing, dashboards, alerts, and production diagnostics.
- When to use: Reliability work, incidents, health checks, bot monitoring, or instrumentation.
- Where it should live: both
- Status: Essential

### secure-code-guardian
- Purpose: Secure coding, auth, authorization, secrets handling, and OWASP-style hardening.
- When to use: Security-sensitive features, user data, API keys, auth flows, or payment-adjacent work.
- Where it should live: both
- Status: Essential

### code-documenter
- Purpose: README work, inline docs, API docs, tutorials, and project handoff documentation.
- When to use: Documentation gaps, onboarding docs, API descriptions, or handoff notes.
- Where it should live: both
- Status: Essential

## Custom skills to consider creating

### deep-planner
- Purpose: A heavier planning skill for large ambiguous projects.
- When to use: Multi-phase or research-heavy planning where standard planning is too shallow.
- Where it should live: `codex-friendly-skills/`
- Status: Missing / placeholder needed

### context-compressor
- Purpose: Compress logs, memory, and state into durable summaries.
- When to use: When project docs or logs are getting noisy or expensive to reread.
- Where it should live: both
- Status: Missing / placeholder needed

### handoff-writer
- Purpose: Turn current work into a clean handoff packet.
- When to use: Before pausing, switching agents, or splitting planning from implementation.
- Where it should live: both
- Status: Missing / placeholder needed

### handoff-reviewer
- Purpose: Validate whether a handoff is complete and actionable.
- When to use: Before giving work to another agent or after receiving a vague handoff.
- Where it should live: both
- Status: Missing / placeholder needed

### project-memory-updater
- Purpose: Update `MEMORY.md`, `PROJECT_STATE.md`, and related files without adding noise.
- When to use: After major milestones or whenever durable context changed.
- Where it should live: both
- Status: Missing / placeholder needed

### prompt-log-compressor
- Purpose: Summarize important prompts and preserve only future-useful context.
- When to use: After long strategy threads, large planning sessions, or repeated user corrections.
- Where it should live: both
- Status: Missing / placeholder needed

### trading-research-architect
- Purpose: Structure trading research systems, data pipelines, and evaluation frameworks.
- When to use: Trading-system design, signal research, or execution research projects.
- Where it should live: `codex-friendly-skills/`
- Status: Optional

### sports-model-architect
- Purpose: Structure sports analytics and modelling workflows.
- When to use: Prediction systems, sports data pipelines, and evaluation frameworks.
- Where it should live: `codex-friendly-skills/`
- Status: Optional

### feature-engineering-reviewer
- Purpose: Review tabular and ML feature engineering for leakage, stability, and usefulness.
- When to use: Before locking feature pipelines or reviewing model-input changes.
- Where it should live: both
- Status: Missing / placeholder needed

### backtest-sanity-checker
- Purpose: Catch invalid assumptions, leakage, lookahead bias, and evaluation mistakes in backtests.
- When to use: Backtesting, research validation, or strategy review.
- Where it should live: `codex-friendly-skills/`
- Status: Missing / placeholder needed

### notification-bot-builder
- Purpose: Build bots for alerts, reports, and notifications.
- When to use: Monitoring bots, scheduled digests, webhook-based messaging, or operations automations.
- Where it should live: both
- Status: Missing / placeholder needed

## Additional installed skill families in this repo

These are already mirrored in `codex-friendly-skills/` and may be useful depending on the project:

- Planning/orchestration: `planner`, `plan-harder`, `swarm-planner`, `parallel-task`, `parallel-task-spark`, `parallel`, `super-swarm-spark`, `llm-council`
- Frontend/design/tooling: `frontend-design`, `frontend-responsive-ui`, `vercel-react-best-practices`, `img-to-frontend`
- Repository/docs/tooling: `openai-docs-skill`, `read-github`, `markdown-url`, `create-hook`, `pluginstaller`, `role-creator`
- Browser/computer use: `agent-browser`, `gemini-computer-use`

Use them only when the task clearly calls for them.
