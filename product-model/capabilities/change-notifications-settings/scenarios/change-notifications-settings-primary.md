---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change notifications settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  actor: user
- text: Personal notification preferences change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Notification settings
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

# Change notifications settings

## Trigger

The User invokes change notifications settings.

## Outcome

Personal notification preferences change

Validated overrides in the notifications section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
