# OTAInspectionApp Decisions And Open Questions

Last updated: 2026-07-03 (encryption fully removed for App Store submission)

> **2026-07-03 update:** All remaining cryptography was removed (SQLCipher, AES-GCM
> local backups/archives, the SecureStore media key, and `expo-secure-store`).
> `ITSAppUsesNonExemptEncryption` is now `false`. Rows and resolved decisions below that
> still say "encrypted backup" or "SQLCipher kept for migration" are superseded by
> `OTAInspectionApp/docs/ENCRYPTION_REMOVAL_2026-07.md`.

## Current Design Decisions In Code

| Area | Current implemented choice | Why it matters |
| --- | --- | --- |
| App model | offline-first, no backend, no login | all trust, storage, and recovery decisions are local-device decisions |
| Navigation | 4 visible tabs plus hidden operational routes | keeps daily flows simple while still exposing export/calendar/storage/permissions tools |
| Persistence boundary | repositories in `data/` | reduces direct screen ownership of storage |
| Inspection storage | normalized plain SQLite tables (migrated from SQLCipher) | supports pagination, child rows, migration logic, and storage metrics |
| Draft storage | single active draft row in DB | fast resume/replace flow without separate screen-owned files |
| Photo storage | JPEG files on disk in `inspection_photos/`, referenced by `media.file_path` (`ota-media://` token); schema migration v4; legacy blobs migrated to disk on first launch | keeps large blobs out of SQLite rows; `inspection_photos/` IS included in OS backup so photos restore with the DB |
| Signature storage | deduplicated base64 blobs in `media` table | preserves signature reuse while keeping render/export simple |
| Database backups | daily **plain** backup (`*.db`) in cache, hash-verified, excluded from OS backup; the live plain DB is what OS backup captures | local corruption-recovery safety copy (encryption removed 2026-07-03) |
| Export model | shared export flow with PDF/CSV/ZIP | one selection model across history, detail, calendar, and storage flows |
| Truck association | explicit `profileId` when possible, fallback truck matching via `sameTruck()` | allows historical inspections to stay attributable even if created before profile cleanup |
| Retention behavior | warning-driven, manual delete from storage screen | avoids silent pruning |
| Permissions | explicit camera/photo/notification service layer | centralizes permission state instead of ad hoc prompts everywhere |
| Theme | static light palette | avoids partially wired theme complexity |
| Android backup | `allowBackup: true` with `data_extraction_rules.xml` (API 31+) and `backup_rules.xml` (API ≤ 30); excludes `secure_media/`, `database_backups/`, `legacy_import_backups/` | the plain SQLite DB and `inspection_photos/` are backed up together; only local-only safety copies are excluded |

## Resolved Decisions

### Database encryption — RESOLVED (Phase 5), then FULLY REMOVED (2026-07-03)

**Decision (2026-07-03):** Plain SQLite with **no encryption machinery at all**. SQLCipher
(`useSQLCipher`) and the `attemptEncryptionMigration` path are removed from `app.json` and
`data/database.ts`. No shipped build ever produced an encrypted database, so there is
nothing to migrate.

**Superseded (Phase 5, 2026-06-24):** previously kept the SQLCipher plugin in `app.json`
for a one-time migration. That is no longer present.

**Rationale:** Encryption adds complexity without a proportional privacy gain for an
app whose data is already behind the device lock screen. Keeping SQLCipher/AES also forced
`ITSAppUsesNonExemptEncryption: true` and an Apple export-compliance flow for no user
benefit. See `OTAInspectionApp/docs/ENCRYPTION_REMOVAL_2026-07.md`.

### Photo storage — RESOLVED (Phase 5 closeout, 2026-06-24)

**Decision:** Photos are stored as JPEG files on disk in `inspection_photos/`, referenced
by `media.file_path`. No AES-256-GCM encryption. 1280 px / JPEG 0.75 (schema migration v4).
`data_base64` is used for signatures only; legacy photo blobs are migrated to disk on first
launch by `migrateBase64PhotosToFilesIfNeeded()` (flag `base64_photo_migration_v1`).

**Rationale:** Encryption was removed for the same reasons as DB encryption. Photos are
stored on disk and excluded from OS backup (`inspection_photos/` is in the backup exclude
lists); they can be re-taken after a restore.

### Android backup — RESOLVED (Phase 5, 2026-06-24)

**Decision:** `android:allowBackup="true"` with explicit XML backup rule files. The
plain SQLite DB is backed up. `inspection_photos/`, `secure_media/`, `database_backups/`,
and `legacy_import_backups/` are excluded from OS backup. Photos are excluded because they
are re-takeable and may reach ~500 MB; backing up photos without the DB (or vice-versa)
would produce orphaned files after a partial restore.

### Retention UX naming — STILL OPEN (low priority)

- `settings.autoDelete` label still says "Retention reminders" in EN (corrected
  from "Auto Delete" in a prior pass). The underlying behavior is warn-only.
- No action required unless the UX needs further clarification.

### Dataset scoping — RESOLVED (Phase 5 closeout, 2026-06-24)

**Decision:** Device-global, single dataset. V1 is one-device-per-driver; no shared-
device use. No scope key, profile/company partition, or multi-user plumbing is added.

**Rationale:** Adding a scope key now would be speculative complexity at the repository
boundary with no current shared-device use case. Revisit only if shared devices become real.

### Release-validation path — RESOLVED, process (Phase 5 closeout, 2026-06-24)

**Decision:** A native EAS development/production build that passes the device
acceptance pass is the release bar. Expo Go is convenience-only and its results do
not count toward release.

**Rationale:** Expo Go masks native camera/share/notification/backup and the
encrypted→plain migration; only a native build exercises them. See
`docs/APP_HARDENING_DEVICE_ACCEPTANCE.md`.

### French terminology review — RESOLVED, process (Phase 5 closeout, 2026-06-24)

**Decision:** Bilingual output is not a legal release gate. No TODO-marked French
string may ship visible at runtime; a fluent/legal terminology review is scheduled as
a fast-follow. See `docs/FR_REVIEW.md`.

**Rationale:** FR users exist but bilingual compliance output is not required; clean
visible strings now, correctness review later.
