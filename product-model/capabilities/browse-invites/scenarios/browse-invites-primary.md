---
kind: primary
routes:
  web-admin: Web administration
  admin-client: Administration API
steps:
- text: The Administrator invokes browse invites.
  kind: actor
  entities:
  - entity: invite
    effect: reads
    facts: []
  contexts: &id001
    web-admin:
      place: web::administration::invites
    admin-client:
      place: client-api::administration
  actor: administrator
- text: Administrative invitation roster returned
  kind: product
  entities:
  - entity: invite
    effect: reads
    facts:
    - Expires at
    - Redeemed at
    - Validity
  - entity: account
    effect: reads
    facts:
    - Username
  contexts: *id001
  actor: administrator
references:
- kind: code
  role: implementation
  target: server/routes/admin.ts
- kind: code
  role: implementation
  target: server/middleware/auth.ts
---

# Browse invites

## Trigger

The Administrator invokes browse invites.

## Outcome

Administrative invitation roster returned

The administrative roster includes expiry, validity and issuer/redeemer association; consumed/expired rows remain until removed.
