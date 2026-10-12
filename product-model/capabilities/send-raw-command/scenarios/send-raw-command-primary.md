---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes send raw command.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: Supported raw IRC command path invoked
  kind: product
  entities:
  - entity: network
    effect: reads
    facts:
    - Connection state
  contexts: *id001
  actor: user
references:
- kind: code
  role: implementation
  target: server/services/wsHub.ts
- kind: code
  role: implementation
  target: server/services/ircManager.ts
- kind: code
  role: implementation
  target: server/db/buffers.ts
- kind: code
  role: implementation
  target: vue_client/src/stores/buffers.ts
- kind: code
  role: implementation
  target: server/services/verbs/sendRaw.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Send raw command

## Trigger

The User invokes send raw command.

## Outcome

Supported raw IRC command path invoked

The supported raw path sanitizes or validates its command and follows surface-specific forwarding/query routing.

## Edge cases

- MCP rejects multiline input and encrypted-channel raw PRIVMSG. That MCP guard is not asserted for the WS raw path.
- Bound bouncer query replies are routed to their requester; post-registration AUTH is not forwarded as ordinary raw IRC.
