---
kind: exception
routes:
  client: Client API
steps:
- text: The User registers a native installation whose sender transport is unavailable.
  kind: actor
  entities: []
  contexts: &id001
    client:
      place: client-api::personal
  actor: user
- text: Unconfigured sender refuses native registration
  kind: product
  entities: []
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

# Register push device sender unavailable

## Trigger

The User registers a native installation whose sender transport is unavailable.

## Outcome

Unconfigured sender refuses native registration
