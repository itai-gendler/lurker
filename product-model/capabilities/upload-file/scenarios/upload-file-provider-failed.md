---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User submits an upload for which the selected provider fails.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: The Product reports the provider failure without claiming successful storage or retained upload history.
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
- kind: code
  role: implementation
  target: server/routes/filehost.ts
---

# Upload file provider failed

## Trigger

The User submits an upload for which the selected provider fails.

## Outcome

Provider failure does not claim successful stored upload
