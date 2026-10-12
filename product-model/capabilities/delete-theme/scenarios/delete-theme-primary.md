---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes delete theme.
  kind: actor
  entities:
  - entity: theme
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::appearance
    client:
      place: client-api::personal
  actor: user
- text: Saved theme removed
  kind: product
  entities:
  - entity: theme
    effect: removes
  - entity: account
    effect: changes
    facts:
    - Appearance settings
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/themesService.ts
- kind: code
  role: implementation
  target: server/db/themes.ts
---

# Delete theme

## Trigger

The User invokes delete theme.

## Outcome

Saved theme removed

Deletion removes the saved theme and resets an appearance selection pointing at that theme.
