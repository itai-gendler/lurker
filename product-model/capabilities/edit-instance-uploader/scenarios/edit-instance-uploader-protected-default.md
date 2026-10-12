---
kind: validation
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator edits a destination in a way that would disable or invalidate the protected default.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::uploaders
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Change violating protected-default constraints refused
  kind: product
  entities: []
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/adminUploaders.ts
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
---

# Edit instance uploader protected default

## Trigger

The Administrator edits a destination in a way that would disable or invalidate the protected default.

## Outcome

Change violating protected-default constraints refused
