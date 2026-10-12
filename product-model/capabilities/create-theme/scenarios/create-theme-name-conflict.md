---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: The User creates a saved appearance snapshot whose name conflicts with an existing saved appearance
    snapshot.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::appearance
    client:
      place: client-api::personal
  actor: user
- text: Conflicting saved name refused
  kind: product
  entities: []
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

# Create theme name conflict

## Trigger

The User creates a saved theme whose name conflicts with an existing saved theme.

## Outcome

Conflicting saved name refused
