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
- text: For a retained registration whose applicable failure budget is exhausted, the Product disables delivery
    and records its health.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: changes
    facts:
    - Delivery health
    - Enabled
  - entity: native-push-device
    effect: changes
    facts:
    - Delivery health
    - Enabled
  contexts: *id001
- text: For a provider-classified expired registration, the Product removes only that expired registration.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: removes
  - entity: native-push-device
    effect: removes
  contexts:
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
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
- kind: code
  role: implementation
  target: server/services/pushService.ts
- kind: code
  role: implementation
  target: server/services/push/index.ts
---

# Deliver notification permanent failure

## Trigger

The Product observes a permanent delivery failure or the applicable failure threshold.

## Outcome

Permanent/threshold failure follows disable/removal policy

## Decision points

### Provider classification

Does the failure identify an expired registration or a retained failure budget? Each branch concerns only the selected transport’s registration.

- Expired registration under the transport’s permanent classification → remove the addressed registration.
- Exhausted retained budget under the applicable policy → retain that registration disabled with recorded health.
