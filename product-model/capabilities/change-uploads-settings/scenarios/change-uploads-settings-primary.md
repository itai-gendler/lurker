---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change uploads settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::uploads-settings
    client:
      place: client-api::personal
  actor: user
- text: Processing/default-destination choices change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Upload settings
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: shared/settingsRegistry.ts
- kind: code
  role: implementation
  target: server/routes/settings.ts
---

# Change uploads settings

## Trigger

The User invokes change uploads settings.

## Outcome

Processing/default-destination choices change

Validated overrides in the uploads section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
