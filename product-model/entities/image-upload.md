---
references:
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
---

# Image upload

An owned stored image upload with dimensions and an optional thumbnail, recorded after provider success.

## Information kept

- **Filename** — The recorded filename.
- **URL** — The returned location of stored bytes.
- **Content type** — The byte-classified content type accepted for this upload.
- **Byte size** — The stored byte size after supported processing.
- **Dimensions** — Recorded image dimensions.
- **Thumbnail** — The optional generated thumbnail or fallback representation.
- **Deletion reference** — Provider deletion information used by the qualified delete operation, omitted from ordinary upload feeds.
- **Favorite status** — Whether the owner starred this upload, including rows later marked removed.
- **Removal status** — Observed removal/tombstone status; this does not imply a mapped public moderation ability.
