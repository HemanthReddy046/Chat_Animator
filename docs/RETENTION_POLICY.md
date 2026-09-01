# Data Retention & Deletion Policy

Status: Binding spec for Phase 10 implementation, defined in Phase 1.

## Default retention

Nothing is retained after a session ends unless the user explicitly clicks "Save project."
Specifically:

| Data | Default lifetime | On explicit "Save project" |
|------|-------------------|------------------------------|
| Raw chat export | Deleted from memory/on-device storage immediately after parsing completes | Never — raw export is never saved, even on explicit save (only the redacted, user-approved summary is) |
| Redacted scene summary | Session only | Retained until user deletes |
| Generated audio (TTS cache) | Session only | Retained until user deletes |
| Rendered video | Session only, available for immediate download | Retained until user deletes |
| Consent confirmation record | Retained as a minimal audit log entry (timestamp + confirmation, no message content) for as long as any related saved project exists | Same |

## What "delete" actually means

Deletion must remove:
- The saved project record and all its assets (summary, audio, video) from primary storage.
- Any on-device cache (IndexedDB / local storage) associated with the project.
- Any server-side log entry that contains content beyond the minimal audit record above.

Deletion must **not** be a soft-delete flag that leaves data recoverable. This is tested
explicitly in Phase 10 by attempting to recover a deleted project through every storage layer
the app uses.

## Why raw chat is never saved, even on "Save project"

The raw chat export is the most sensitive artifact in this entire pipeline — it's other
people's private words, not just the user's. Keeping the redacted summary (which the user has
already reviewed and approved) is sufficient to let them revisit or re-render a project;
keeping the raw chat is not, and it is the single highest-value thing to minimize under the
DPDP Act's data minimisation principle. This is a deliberate product limitation, not a
missing feature.
