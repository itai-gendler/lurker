---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes export network certificate.
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
- text: Owned certificate and private credential exported
  kind: product
  entities:
  - entity: network-certificate
    effect: reads
    facts:
    - Certificate
    - Private credential
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

# Export network certificate

## Trigger

The User invokes export network certificate.

## Outcome

Owned certificate and private credential exported

The certificate and private credential are returned through the qualified owned download with no-store handling.
