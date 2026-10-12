---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes unfavorite upload.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: For the selected content class, the Product applies the selected-image or selected-file operation.
    Owned star removed
  kind: product
  entities:
  - entity: image-upload
    effect: changes
    facts:
    - Favorite status
  - entity: file-upload
    effect: changes
    facts:
    - Favorite status
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/uploads.ts
- kind: code
  role: implementation
  target: server/services/uploadService.ts
- kind: code
  role: implementation
  target: server/db/uploadHistory.ts
---

# Unfavorite upload

## Trigger

The User invokes unfavorite upload.

## Outcome

Owned star removed

The selected owned image or file’s star changes. The endpoint can update a removed owned row even though favorite feeds exclude removed rows.
