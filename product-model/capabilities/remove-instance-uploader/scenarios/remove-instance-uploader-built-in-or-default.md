---
kind: validation
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator tries to remove a built-in destination or the current default.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::uploaders
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Built-in/default protected destination cannot be removed
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

# Remove instance uploader built in or default

## Trigger

The Administrator tries to remove a built-in destination or the current default.

## Outcome

Built-in/default protected destination cannot be removed
