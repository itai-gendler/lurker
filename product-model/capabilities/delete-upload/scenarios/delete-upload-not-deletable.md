---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User tries to delete an upload that is nonowned, removed or lacks a usable deletion reference.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: For the selected content class, the Product applies the selected-image or selected-file operation.
    Nonowned, removed or otherwise nondeletable record refused
  kind: product
  entities: []
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

# Delete upload not deletable

## Trigger

The User tries to delete an upload that is nonowned, removed or lacks a usable deletion reference.

## Outcome

Nonowned, removed or otherwise nondeletable record refused
