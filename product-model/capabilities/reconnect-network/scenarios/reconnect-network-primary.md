---
kind: primary
routes:
  web: Web
  client: Client API
steps:
- text: The User invokes reconnect network.
  kind: actor
  entities:
  - entity: network
    effect: reads
    facts: []
  contexts: &id001
    web:
      place: web::personal::network
    client:
      place: client-api::personal
  actor: user
- text: Existing connection replaced and a fresh connection requested
  kind: product
  entities:
  - entity: network
    effect: changes
    facts:
    - Connection state
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/routes/networks.ts
- kind: code
  role: implementation
  target: server/db/networks.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/services/verbs/connectNetwork.ts
---

# Reconnect network

## Trigger

The User invokes reconnect network.

## Outcome

Existing connection replaced and a fresh connection requested

The host/proxy policy and account state are checked before requesting a dial. Reconnect replaces the prior connection; MCP force:true is its reconnect path.

## Edge cases

- Registration and later failure arrive asynchronously; request acceptance is not confirmed connection success.
