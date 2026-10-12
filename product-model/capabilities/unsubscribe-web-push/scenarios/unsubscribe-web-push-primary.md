---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes unsubscribe web push.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  actor: user
- text: When the addressed registration is web push subscription, the Product removes that owner-and-endpoint match.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: removes
  contexts: *id001
  actor: user
- text: When the same addressed owner-and-endpoint match has the other stored transport, the Product removes that
    matching registration.
  kind: product
  entities:
  - entity: native-push-device
    effect: removes
  contexts:
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/push.ts
- kind: code
  role: implementation
  target: server/db/pushSubscriptions.ts
---

# Unsubscribe web push

## Trigger

The User invokes unsubscribe web push.

## Outcome

Owned endpoint registration removed

Both deletion routes use the same owner-and-endpoint lookup without a transport predicate. Only the matched registration is removed; an absent or differently owned endpoint leaves registrations unchanged and returns the route’s success response. This does not establish a separate native web registration ceremony.
