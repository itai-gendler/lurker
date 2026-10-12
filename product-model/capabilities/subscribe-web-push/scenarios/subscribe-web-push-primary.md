---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes subscribe web push.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  actor: user
- text: For a new endpoint, the Product records Web Push delivery keys, device description, enabled defaults, seen
    time, delivery health and authorization association.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: creates
    facts:
    - Endpoint
    - Delivery keys
    - Device description
    - Enabled
    - Last seen at
    - Delivery health
    - Authorization association
    as: new-web-push-subscription
  contexts: *id001
  actor: user
- text: For the same transport class, for the same registered endpoint, the Product replaces delivery keys and the
    latest authorization association, preserves an omitted device description, enables delivery and resets health.
  kind: product
  entities:
  - entity: web-push-subscription
    effect: changes
    facts:
    - Delivery keys
    - Device description
    - Enabled
    - Last seen at
    - Delivery health
    - Authorization association
    as: existing-web-push-subscription
  contexts:
    web:
      place: web::personal::notifications
    client:
      place: client-api::personal
  actor: user
- text: When a same-owner endpoint registration changes transport class, the Product replaces the predecessor’s
    transport-specific subject with the accepted incoming registration.
  kind: product
  entities:
  - entity: native-push-device
    effect: removes
  - entity: web-push-subscription
    effect: creates
    facts:
    - Endpoint
    - Delivery keys
    - Device description
    - Enabled
    - Last seen at
    - Delivery health
    - Authorization association
    as: replacement-web-push-subscription
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
- kind: code
  role: implementation
  target: server/services/pushService.ts
- kind: code
  role: implementation
  target: server/services/push/index.ts
- kind: code
  role: implementation
  target: server/services/wsHub.ts
---

# Subscribe web push

## Trigger

The User invokes subscribe web push.

## Outcome

Web Push endpoint/keys registered under endpoint ownership rules

Validated endpoint and delivery keys register or refresh the account’s Web Push delivery association.

## Edge cases

- Ordinary browser cross-account endpoints refuse registration. Both stored and incoming Web Push registrations naming a relay device may rebind when the relay policy admits them.

## Decision points

### Existing selected record

Does the selected record already exist?

- Absent record → create it with its supported initial/default values.
- Existing same-class record → update that selected record without an independent duplicate.
- Existing other-class record owned by this same account → overwrite the endpoint’s transport-specific registration using the validated incoming fields; this does not delete a provider endpoint.
