---
kind: path
routes:
  web: Web
  client: Client API
steps:
- text: The User edits a personal destination while omitting a replacement secret.
  kind: actor
  entities:
  - entity: personal-uploader
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::uploads-settings
    client:
      place: client-api::personal
  actor: user
- text: Omitted secret preserves existing value
  kind: product
  entities:
  - entity: personal-uploader
    effect: changes
    facts:
    - Label
    - Configuration
    - Secret status
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/uploaders.ts
- kind: code
  role: implementation
  target: server/db/uploaderConfig.ts
- kind: code
  role: implementation
  target: server/services/uploadProviders/resolve.ts
---

# Edit personal uploader omitted secret retained

## Trigger

The User edits a personal destination while omitting a replacement secret.

## Outcome

Omitted secret preserves existing value
