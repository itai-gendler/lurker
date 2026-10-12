---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User requests deletion but the provider fails to delete the stored bytes.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: For the selected content class, the Product applies the selected-image or selected-file operation.
    Failed byte deletion leaves history intact
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

# Delete upload provider failed

## Trigger

The User requests deletion but the provider fails to delete the stored bytes.

## Outcome

Failed byte deletion leaves history intact
