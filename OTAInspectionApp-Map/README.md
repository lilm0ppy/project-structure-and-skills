# OTAInspectionApp Map

This folder is the working map for the current `OTAInspectionApp/` workspace as analyzed on `2026-06-24`.

It documents the local app worktree, not just the last commit. The app repo is intentionally dirty and currently contains substantial uncommitted work, so these notes are based on the live source in the workspace.

## Read Order

1. [APP_CONTEXT.md](APP_CONTEXT.md)
2. [ARCHITECTURE_AND_DATA_FLOW.md](ARCHITECTURE_AND_DATA_FLOW.md)
3. [PROJECT_STATE.md](PROJECT_STATE.md)
4. [DECISIONS_AND_OPEN_QUESTIONS.md](DECISIONS_AND_OPEN_QUESTIONS.md)

## Fast Takeaways

- The app is an offline-first Expo/React Native mobile app for Ontario Schedule 1 truck inspections.
- The original AsyncStorage-only design has evolved into a normalized SQLite repository layer, encrypted photo storage, recovery tooling, export pipelines, a calendar surface, a permissions surface, and a storage-health surface.
- The strongest source of truth is now the code under `data/`, `hooks/`, `services/`, and `app/`, with tests in `__tests__/` backing much of that behavior.
- Several app-internal docs are directionally useful but stale in important places. The biggest drift is that runtime database behavior is no longer the same as the older "fully encrypted SQLCipher runtime" description.
- Current automated checks pass: `npm test -- --runInBand` (`23/23` suites, `74/74` tests), `npx tsc --noEmit`, and `npx expo-doctor` (`18/18`).

## Source Hierarchy

1. Runtime code in `OTAInspectionApp/data/`, `hooks/`, `services/`, `app/`
2. Tests in `OTAInspectionApp/__tests__/`
3. App docs in `OTAInspectionApp/docs/`
4. Original product intent in `project start.md`

## Known Drift To Keep In Mind

- Multiple app docs still say the live database is encrypted with SQLCipher. The current runtime code in `data/database.ts` migrates encrypted databases to plain SQLite and only applies `PRAGMA key` as a fallback when that migration fails.
- Some older hardening notes assume `android.allowBackup=false`, but the current `app.json` sets `android.allowBackup: true`.
- Some UI copy still says "Auto Delete" even though current behavior is warning plus manual cleanup, not automatic pruning.
