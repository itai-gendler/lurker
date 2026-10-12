---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes add instance uploader.
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
- text: Instance destination created
  kind: product
  entities:
  - entity: instance-uploader
    effect: creates
    facts:
    - Label
    - Driver
    - Configuration
    - Secrets
    - Secret status
    - Enabled
    - Offered to users
    - Default status
    - Managed status
    - Built-in status
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

# Add instance uploader

## Trigger

The Administrator invokes add instance uploader.

## Outcome

Instance destination created
