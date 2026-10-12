---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change input bar settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::input-bar
    client:
      place: client-api::personal
  actor: user
- text: Input preferences change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Input bar settings
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

# Change input bar settings

## Trigger

The User invokes change input bar settings.

## Outcome

Input preferences change

Validated overrides in the input bar section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
