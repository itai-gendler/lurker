---
kind: primary
routes:
  web: Web
steps:
- text: The User invokes browse bouncer settings.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::bouncer
  actor: user
- text: Authenticated connection details shown
  kind: product
  entities:
  - entity: instance-settings
    effect: reads
    facts:
    - Bouncer connection details
    - Feature availability
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/bouncer.ts
- kind: code
  role: implementation
  target: server/routes/config.ts
---

# Browse bouncer settings

## Trigger

The User invokes browse bouncer settings.

## Outcome

Authenticated connection details shown
