---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes change appearance settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::appearance
    client:
      place: client-api::personal
  actor: user
- text: Appearance overrides/theme selection change
  kind: product
  entities:
  - entity: account
    effect: changes
    facts:
    - Appearance settings
  - entity: theme
    effect: reads
    facts: []
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

# Change appearance settings

## Trigger

The User invokes change appearance settings.

## Outcome

Appearance overrides/theme selection change

Validated overrides in the appearance section are saved for the account and synchronized. Omitted preferences retain the registry-driven defaults.
