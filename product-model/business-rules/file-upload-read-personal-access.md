---
appliesTo:
- type: entity
  id: file-upload
  effect: reads
  contexts:
  - place: web::personal
  - place: client-api::personal
  facts:
  - Filename
  - URL
  - Content type
  - Byte size
  - Favorite status
  - Removal status
permits:
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: user
- related:
  - verb: owns
    entity: account
  - verb: has-account
    entity: administrator
references:
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
---

# File upload disclosure requires the stated owner or bound entry authority

Same operation boundaries, excluding image-only facts.
