---
kind: path
routes:
  web: Web
  client: Client API
steps:
- text: The User submits a valid certificate pair while an existing pair is attached.
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
- text: Valid replacement pair replaces prior attachment
  kind: product
  entities:
  - entity: network-certificate
    effect: removes
    from: Attached
  contexts: *id001
  actor: user
- text: The Product attaches the validated replacement pair.
  kind: product
  entities:
  - entity: network-certificate
    effect: creates
    facts:
    - Certificate description
    - Certificate
    - Private credential
    to: Attached
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

# Set network certificate replace certificate

## Trigger

The User submits a valid certificate pair while an existing pair is attached.

## Outcome

Valid replacement pair replaces prior attachment
