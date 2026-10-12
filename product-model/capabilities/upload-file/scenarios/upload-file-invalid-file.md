---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User submits bytes rejected by type, size, classification or upload policy.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads
    client:
      place: client-api::personal
  actor: user
- text: The Product refuses the input before storing an upload.
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

# Upload file invalid file

## Trigger

The User submits bytes rejected by type, size, classification or upload policy.

## Outcome

Invalid bytes/type/size/policy input refused
