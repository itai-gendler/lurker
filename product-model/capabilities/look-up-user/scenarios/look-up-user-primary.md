---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: The User invokes look up user.
  kind: actor
  entities: []
  contexts: &id001
    web:
      place: web::personal::profile
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  actor: user
- text: The Product requests profile information with WHOIS; attributable replies can supply a partial profile
    or asynchronous output.
  kind: product
  entities:
  - entity: irc-user
    effect: reads
    facts:
    - Profile information
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
  target: server/services/verbs/whois.ts
---

# Look up user

## Trigger

The User invokes look up user.

## Outcome

WHOIS requested; profile or asynchronous result exposed

WHOIS requests observation. Web/profile results can be partial; MCP acknowledges the outbound request and later output requires a separate history read.

## Edge cases

- MCP has no asynchronous stream and does not automatically perform that later read.
