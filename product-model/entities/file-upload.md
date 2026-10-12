---
references:
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
---

# File upload

An owned stored media or text upload. Both retain the same information, without image-only dimensions or thumbnails.

## Information kept

- **Filename** — The recorded filename.
- **URL** — The returned location of stored bytes.
- **Content type** — The byte-classified content type accepted for this upload.
- **Byte size** — The stored byte size after supported processing.
- **Deletion reference** — Provider deletion information used by the qualified delete operation, omitted from ordinary upload feeds.
- **Favorite status** — Whether the owner starred this upload, including rows later marked removed.
- **Removal status** — Observed removal/tombstone status; this does not imply a mapped public moderation ability.
