---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes create theme.
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
- text: Named theme snapshot saved
  kind: product
  entities:
  - entity: theme
    effect: creates
    facts:
    - Name
    - Values
    - Created at
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

# Create theme

## Trigger

The User invokes create theme.

## Outcome

Named theme snapshot saved

A valid named values snapshot is saved under the account’s theme-name and count limits.
