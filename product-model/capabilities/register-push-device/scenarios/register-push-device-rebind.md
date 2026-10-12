---
kind: path
routes:
  client: Client API
steps:
- text: The User registers an installation token under the supported stored and incoming native-device transport
    combination.
  kind: actor
  entities: []
  contexts: &id001
    client:
      place: client-api::personal
  actor: user
- text: When both registrations are native, the presented installation token rebinds to the signing-in account.
    Mixed native/Web Push collisions remain distinct refusals.
  kind: product
  entities:
  - entity: native-push-device
    effect: changes
    facts:
    - Transport
    - Installation token
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

# Register push device rebind

## Trigger

The User registers an installation token under the supported stored and incoming native-device transport combination.

## Outcome

When both registrations are native, the presented installation token rebinds to the signing-in account. Mixed native/Web Push collisions remain distinct refusals.
