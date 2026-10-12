---
kind: path
routes:
  web: Web
  client: Client API
steps:
- text: The User deletes the saved theme currently selected for appearance.
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
- text: Deleting selected saved theme resets its selection pointer
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

# Delete theme selected pointer reset

## Trigger

The User deletes the saved theme currently selected for appearance.

## Outcome

Deleting selected saved theme resets its selection pointer
