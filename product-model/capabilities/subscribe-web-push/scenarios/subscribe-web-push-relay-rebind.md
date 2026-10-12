---
kind: path
routes:
  client: Client API
steps:
- text: The User registers a relay-device Web Push endpoint whose existing registration is also a relay device
    on another member identity.
  kind: actor
  entities: []
  contexts: &id001
    client:
      place: client-api::personal
  actor: user
- text: When both the stored and incoming registrations are Web Push and the endpoint names a relay device,
    the signing-in account takes the registration, replaces delivery keys/authorization association and resets
    health.
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

# Subscribe web push relay rebind

## Trigger

The User registers a relay-device Web Push endpoint whose existing registration is also a relay device on another account.

## Outcome

When both the stored and incoming registrations are Web Push and the endpoint names a relay device, the signing-in account takes the registration, replaces delivery keys/authorization association and resets health.
