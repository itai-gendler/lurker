---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes browse authorized apps.
  kind: actor
  entities:
  - entity: authorized-app
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::authorized-apps
    client:
      place: client-api::personal
  actor: user
- text: Owned application authorizations returned
  kind: product
  entities:
  - entity: authorized-app
    effect: reads
    facts:
    - Approval
    - Last used at
  - entity: client-application
    effect: reads
    facts:
    - Name
    - Website
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/oauth.ts
- kind: code
  role: implementation
  target: server/db/oauth.ts
---

# Browse authorized apps

## Trigger

The User invokes browse authorized apps.

## Outcome

Owned application authorizations returned
