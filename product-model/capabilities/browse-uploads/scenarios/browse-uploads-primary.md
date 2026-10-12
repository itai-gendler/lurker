---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes browse uploads.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: Owned upload history/favorites returned
  kind: product
  entities:
  - entity: image-upload
    effect: reads
    facts:
    - Filename
    - URL
    - Content type
    - Byte size
    - Dimensions
    - Thumbnail
    - Favorite status
    - Removal status
  - entity: file-upload
    effect: reads
    facts:
    - Filename
    - URL
    - Content type
    - Byte size
    - Favorite status
    - Removal status
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

# Browse uploads

## Trigger

The User invokes browse uploads.

## Outcome

Owned upload history/favorites returned

Owned history supports the implemented content filters, search, before cursor and favorite projection. Ordinary feeds omit deletion references.

## Edge cases

- Removed rows are excluded from favorite feeds but may remain in their supported history projection.
