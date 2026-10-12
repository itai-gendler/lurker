---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes remove network certificate.
  kind: actor
  entities:
  - entity: network-certificate
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::network
    client:
      place: client-api::personal
  actor: user
- text: Current certificate pair detached
  kind: product
  entities:
  - entity: network-certificate
    effect: removes
    from: Attached
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
---

# Remove network certificate

## Trigger

The User invokes remove network certificate.

## Outcome

Current certificate pair detached
