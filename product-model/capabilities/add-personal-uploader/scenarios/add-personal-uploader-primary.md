---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes add personal uploader.
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
- text: Allowed owned destination configuration created
  kind: product
  entities:
  - entity: personal-uploader
    effect: creates
    facts:
    - Label
    - Driver
    - Configuration
    - Secrets
    - Secret status
    - Enabled
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

# Add personal uploader

## Trigger

The User invokes add personal uploader.

## Outcome

Allowed owned destination configuration created

Personal destination configuration follows the supported driver and creation policy. Configuration responses omit secret values; omitted replacement secrets retain existing values.

## Edge cases

- Disabling personal creation does not forbid editing/removing already-owned destinations. Effective selected destination falls back to the allowed instance default when needed.
