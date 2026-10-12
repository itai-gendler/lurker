---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes delete upload.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: For the selected content class, the Product applies the selected-image or selected-file operation.
    Provider deletion succeeds before history removal
  kind: product
  entities:
  - entity: image-upload
    effect: removes
  - entity: file-upload
    effect: removes
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

# Delete upload

## Trigger

The User invokes delete upload.

## Outcome

Provider deletion succeeds before history removal

Only the selected image or file row is removed, after its configured provider deletion succeeds.

## Edge cases

- A missing destination/configuration can make a record nondeletable. Provider deletion failure preserves the retained history row.
