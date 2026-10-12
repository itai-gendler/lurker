---
appliesTo:
- type: entity
  id: image-upload
  effect: reads
  contexts:
  - place: web::personal
  - place: client-api::personal
  facts:
  - Filename
  - URL
  - Content type
  - Byte size
  - Dimensions
  - Thumbnail
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

# Image upload disclosure requires the stated owner or bound entry authority

Accepted authenticated upload; owned history versus public key-addressed bytes; owned favorite changes; owned nonremoved deletable row after successful provider deletion.
