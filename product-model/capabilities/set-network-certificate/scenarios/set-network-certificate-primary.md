---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes set network certificate.
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
- text: Valid generated/imported certificate pair attached
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

# Set network certificate

## Trigger

The User invokes set network certificate.

## Outcome

Valid generated/imported certificate pair attached

A generated or imported matching certificate/private-key pair is attached to a TLS-enabled network and used on a subsequent connection.

## Edge cases

- Invalid pairs and non-TLS attachment are refused. Attaching does not itself cycle the existing connection.
