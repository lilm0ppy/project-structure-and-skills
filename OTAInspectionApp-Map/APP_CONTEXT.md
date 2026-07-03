# OTAInspectionApp Context

## What The App Is

`OTAInspectionApp` is a local-first mobile app for daily Ontario Trucking Association vehicle inspection reports. It is meant to replace paper Schedule 1 logs for drivers who need to create, retain, review, and export inspections while offline.

The original product scope was a lightweight Expo app with local storage, profile autofill, signatures, and PDF export. The current workspace has grown into a more operationally hardened app with repositories, migration/import logic, media encryption, recovery surfaces, calendar filtering, export bundles, and storage diagnostics.

## Current Runtime Stack

| Area | Current implementation |
| --- | --- |
| Framework | Expo SDK `54.0.35` |
| UI runtime | React Native `0.81.5`, React `19.1.0` |
| Routing | `expo-router` file-based routes |
| Persistence | `expo-sqlite` database plus filesystem media and export artifacts |
| Legacy migration source | AsyncStorage keys under `utils/storage.ts` |
| Device secrets | `expo-secure-store` |
| Photo capture | `expo-image-picker` + `expo-image-manipulator` |
| PDF/export | `expo-print`, `expo-sharing`, custom CSV/ZIP services |
| Notifications | `expo-notifications` |
| Signature capture | `react-native-signature-canvas` |
| Testing | Jest + `sql.js` fixtures for repository tests |

## Primary User Flows

- Manage reusable truck/company/driver profiles and a saved signature.
- Start or resume a daily inspection.
- Mark checklist items as `ok`, `defect`, or `major`, with comments and optional photos.
- Submit an inspection tied to a truck identity and historical snapshot fields.
- Add same-day en-route defects from the home screen.
- Review records in history and calendar views.
- Export one inspection or a filtered range as PDF, CSV, or ZIP bundle.
- Monitor storage pressure, cleanup state, permissions, and quarantine/recovery state.

## Route Map

| Route | Surface type | Purpose |
| --- | --- | --- |
| `app/index.tsx` | visible tab | home dashboard, today's inspection, quick-add defect, recent history |
| `app/history.tsx` | visible tab | paged history list, range export, copy as text |
| `app/settings.tsx` | visible tab | language, units, reminders, retention warnings, storage, permissions |
| `app/profile.tsx` | visible tab | truck profile CRUD and active truck selection |
| `app/new-inspection.tsx` | hidden route | create/resume inspection, autosave, submit |
| `app/view-inspection.tsx` | hidden route | read-only inspection detail, export |
| `app/storage-offline.tsx` | hidden route | storage metrics, cleanup, retention-delete flow, quarantine export |
| `app/calendar.tsx` | hidden route | month/day inspection navigation with truck filters |
| `app/permissions.tsx` | hidden route | camera/photos/notifications status and settings handoff |
| `app/_layout.tsx` | layout | error boundary, `DataProvider`, `AppSettingsProvider`, tab shell |

## Folder Map

| Folder | File count | Role |
| --- | ---: | --- |
| `app/` | 10 | routes and UI surfaces |
| `components/` | 12 | reusable UI blocks and flow sheets |
| `constants/` | 4 | checklist data, colors, app constants, translations |
| `data/` | 15 | database, repositories, migration, integrity, backup |
| `hooks/` | 5 | UI-facing adapters over repositories/services |
| `services/` | 7 | export, permissions, notifications, recovery flows |
| `types/` | 2 | shared runtime and export contracts |
| `utils/` | 11 | helpers for inspections, dates, storage, photos, PDF text |
| `docs/` | 8 | app-local handoffs, hardening notes, privacy policy |
| `__tests__/` | 24 | repository, export, migration, crypto, autosave, and helper coverage |

## Core Domain Model

| Model | Meaning |
| --- | --- |
| `TruckProfile` | saved truck/company/driver defaults plus saved signature and active-truck identity |
| `InspectionRecord` | immutable submitted inspection snapshot, including header fields, defect states, summaries, signatures, remarks, and truck linkage |
| `DefectItem` | one checklist item with status, comments, and optional photo tokens |
| `EnRouteDefect` | same-day defect added after submission from the home screen |
| `ExportSelection` | export filter contract covering range, trucks, format, photos, and detail level |
| `PreparedExport` | staged export artifact ready for the share sheet |

## Checklist Scope

- `23` checklist categories
- `75` total checklist items
- `46` items marked as major-defect-capable

## Product Evolution From The Original Spec

The original `project start.md` expected:

- AsyncStorage for profiles and inspection history
- 5 main screens
- 14-day local retention focus
- simple PDF sharing

The current workspace now includes:

- a normalized SQLite schema with migrations and repository access
- a legacy AsyncStorage import path
- encrypted photo storage and deduplicated signature storage
- integrity checks, quarantine, verified backups, and a recovery export
- history pagination, calendar aggregation, and storage metrics
- PDF, CSV, and ZIP bundle export with manifest hashing
- operational screens for permissions and storage/offline state

## Important Truth Source Notes

- Use code first when app-local docs disagree with runtime behavior.
- Treat `data/` as the persistence boundary.
- Treat `services/export/` as the export boundary.
- Treat `app/new-inspection.tsx` as the main write flow and `useInspections()` plus `inspectionRepository.ts` as the main read/write backbone.
