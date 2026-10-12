---
kind: validation
routes:
  web: Web
  client: Client API
steps:
- text: The User registers an ordinary browser endpoint already owned by another member identity.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  actor: user
- text: Ordinary browser endpoint owned by another account refused
  kind: product
  entities:
  - entity: account
    effect: reads
    facts: []
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
---

# Subscribe web push endpoint conflict

## Trigger

The User registers an ordinary browser endpoint already owned by another account.

## Outcome

Ordinary browser endpoint owned by another account refused
