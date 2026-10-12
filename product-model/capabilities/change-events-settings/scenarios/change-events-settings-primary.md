---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change events settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::events
    client:
      place: client-api::personal
  actor: user
- text: Event-display preferences change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Event settings
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

# Change events settings

## Trigger

The User invokes change events settings.

## Outcome

Event-display preferences change

Validated overrides in the events section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
