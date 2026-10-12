---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change data settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::data
    client:
      place: client-api::personal
  actor: user
- text: Retention preferences change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Data settings
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

# Change data settings

## Trigger

The User invokes change data settings.

## Outcome

Retention preferences change

Validated overrides in the data section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
