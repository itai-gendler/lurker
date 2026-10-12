---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change away settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::away
    client:
      place: client-api::personal
  actor: user
- text: Automatic-away/scope preferences change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Away settings
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

# Change away settings

## Trigger

The User invokes change away settings.

## Outcome

Automatic-away/scope preferences change

Validated overrides in the away section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
