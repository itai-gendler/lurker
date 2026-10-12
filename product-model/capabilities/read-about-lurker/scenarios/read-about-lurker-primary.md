---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes read about lurker.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::about
    client:
      place: client-api::personal
  actor: user
- text: Authenticated application/engine information returned
  kind: product
  entities:
  - entity: instance-settings
    effect: reads
    facts:
    - Versions
    - Edition
    - Feature availability
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/about.ts
- kind: code
  role: implementation
  target: server/protocol.ts
---

# Read about lurker

## Trigger

The User invokes read about lurker.

## Outcome

Authenticated application/engine information returned
