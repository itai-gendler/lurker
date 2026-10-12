---
kind: primary
routes:
  client: Client API
steps:
- text: The User invokes unregister push device.
  kind: actor
  entities: []
  contexts: &id001
    client:
      place: client-api::personal
  actor: user
- text: When the addressed registration is native push device, the Product removes that owner-and-endpoint match.
  kind: product
  entities:
  - entity: native-push-device
    effect: removes
  contexts: *id001
  actor: user
- text: When the same addressed owner-and-endpoint match has the other stored transport, the Product removes that
    matching registration.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: removes
  contexts:
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

# Unregister push device

## Trigger

The User invokes unregister push device.

## Outcome

Registration matching owner and endpoint removed

Deregistration matches owner plus endpoint without an additional transport predicate.

Both deletion routes use the same owner-and-endpoint lookup without a transport predicate. Only the matched registration is removed; an absent or differently owned endpoint leaves registrations unchanged and returns the route’s success response. This does not establish a separate native web registration ceremony.
