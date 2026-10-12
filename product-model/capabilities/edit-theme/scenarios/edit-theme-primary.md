---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes edit theme.
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
- text: Saved theme name/values changed
  kind: product
  entities:
  - entity: theme
    effect: changes
    facts:
    - Name
    - Values
    - Updated at
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

# Edit theme

## Trigger

The User invokes edit theme.

## Outcome

Saved theme name/values changed
