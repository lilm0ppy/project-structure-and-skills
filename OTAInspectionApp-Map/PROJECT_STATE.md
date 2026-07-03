# OTAInspectionApp Project State

## Snapshot

- Analysis date: `2026-06-24`
- Scope: current local `OTAInspectionApp/` worktree, including uncommitted changes
- Git state: intentionally dirty; this map describes the live workspace, not a clean release commit
- Product stage: functionally rich offline inspection app with hardening/recovery work already present in code

## Verified Checks

- `npm test -- --runInBand`
  - result: `23/23` suites passed, `74/74` tests passed
  - known noise:
    - one expected quarantine `console.warn` in `legacyImportProfiles.test.ts`
    - React act-environment warnings during `useAutosave.test.tsx`
- `npx tsc --noEmit`
  - result: passed
- `npx expo-doctor`
  - result: `18/18` checks passed

## What Is In Good Shape

- There is now a real persistence boundary under `data/` instead of raw screen-owned storage logic.
- Inspection metadata is normalized into tables with child rows for checklist items, summaries, en-route defects, drafts, and export history.
- Photo handling is materially stronger than the original design:
  - compression on ingest
  - encrypted photo payloads
  - secure token references instead of plain file paths in the record model
  - temporary decrypted cache cleanup
- Legacy AsyncStorage import is non-trivial and intentionally cautious:
  - quarantine on invalid JSON
  - verification before source deletion
  - encrypted archive of imported legacy source data
- Export behavior is much more mature than the original spec:
  - PDF, CSV, ZIP bundle
  - semantic manifest hashing
  - truck/date filtering
  - bounded photo embedding
  - progress and cancellation behavior
- Test coverage is strongest around the data layer, export behavior, crypto helpers, migrations, and autosave behavior.

## What Is Still Fragile Or Needs Clarification

### 1. Runtime behavior and app docs are not fully aligned

- `data/database.ts` now migrates previously encrypted databases to plain SQLite and normally runs without `PRAGMA key`.
- Several docs in `OTAInspectionApp/docs/` still describe a native encrypted SQLCipher runtime.
- Result: future work could easily be planned against the wrong security model unless code is treated as the source of truth.

### 2. Android backup policy is unclear

- Current `app.json` sets `android.allowBackup: true`.
- Several older hardening notes describe `allowBackup=false`.
- This matters for privacy, disaster recovery, and how seriously the app is treating local sensitive data.

### 3. Retention naming no longer matches behavior

- The settings UI still uses `auto delete` language.
- Current behavior is warning-plus-manual-delete from the storage screen.
- History cards still show an `older than 14 days` style message while retention is now configurable.

### 4. Native acceptance is still outstanding

Automated checks pass, but the codebase still needs device-level validation for:

- iOS and Android native builds
- camera / photo-library permission flows
- notification permission flows
- native share sheet behavior
- low-storage behavior
- process-kill draft recovery
- backup / restore expectations

### 5. Some translation/legal review work remains

- `constants/ChecklistData.ts` still contains explicit TODOs for human review of French Schedule 1 terminology.
- That is not a code blocker, but it is still product debt if French output is meant to be trusted in a compliance context.

## Most Important Current Codebase Truths

- `data/` is the most important architectural boundary in the app.
- `useInspections()` and `inspectionRepository.ts` are the main inspection read/write path.
- `app/new-inspection.tsx` is the write-heavy UX surface and the best single file for understanding submission flow.
- `services/export/` plus `utils/pdfTemplate.ts` own export behavior.
- `storage-offline.tsx` is the operational surface for cleanup, retention delete, storage pressure, and quarantine export.

## Safe Assumptions For Future Work

- Do not assume app-local docs are current if they disagree with code.
- Do not assume the database is encrypted at rest today just because SQLCipher support is still configured.
- Do not treat the retention setting as automatic deletion unless the code is changed to make it so.
- Do not start behavior changes in the screen layer first if the behavior obviously belongs to persistence, media, export, or notifications.

## Recommended Next Decision Window

Before major feature work, the owner should answer the open questions in [DECISIONS_AND_OPEN_QUESTIONS.md](DECISIONS_AND_OPEN_QUESTIONS.md), especially:

- live database encryption policy
- Android backup policy
- retention UX semantics
- native-build validation expectations
