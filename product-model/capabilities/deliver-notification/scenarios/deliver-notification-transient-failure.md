---
kind: exception
routes:
  web: Web
  client: Client API
steps:
- text: Recorded activity reaches the notification eligibility check.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  unattended: true
- text: Transient provider failure updates health without immediate permanent deletion
  kind: product
  entities:
  - entity: web-push-subscription
    effect: changes
    facts:
    - Delivery health
  - entity: native-push-device
    effect: changes
    facts:
    - Delivery health
  contexts: *id001
references:
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
- kind: code
  role: implementation
  target: server/services/push/relay.ts
---

# Deliver notification transient failure

## Trigger

The Product attempts eligible notification delivery and receives a transient provider failure.

## Outcome

Transient provider failure updates health without immediate permanent deletion
