---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes remove instance uploader.
  kind: actor
  entities:
  - entity: instance-uploader
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::uploaders
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Permitted destination removed
  kind: product
  entities:
  - entity: instance-uploader
    effect: removes
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

# Remove instance uploader

## Trigger

The Administrator invokes remove instance uploader.

## Outcome

Permitted destination removed

Standalone deletion preserves built-in and current default destinations.
