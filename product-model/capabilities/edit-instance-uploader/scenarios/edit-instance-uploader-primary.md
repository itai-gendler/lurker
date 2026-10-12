---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes edit instance uploader.
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
- text: Permitted instance configuration changed
  kind: product
  entities:
  - entity: instance-uploader
    effect: changes
    facts:
    - Label
    - Driver
    - Configuration
    - Secrets
    - Secret status
    - Enabled
    - Offered to users
    - Default status
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

# Edit instance uploader

## Trigger

The Administrator invokes edit instance uploader.

## Outcome

Permitted instance configuration changed

Standalone configuration follows managed-row and protected-default restrictions. Responses redact secrets and locked configuration; omitted secrets retain the prior value.
