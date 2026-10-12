---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes change uploaders settings.
  kind: actor
  entities: []
  contexts: &id001
    web-admin:
      place: web::administration::uploaders
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Personal-creation policy/default changes
  kind: product
  entities:
  - entity: instance-settings
    effect: changes
    facts:
    - Uploader policy
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

# Change uploaders settings

## Trigger

The Administrator invokes change uploaders settings.

## Outcome

Personal-creation policy/default changes

Standalone personal-creation policy and default selection change under default continuity constraints.
