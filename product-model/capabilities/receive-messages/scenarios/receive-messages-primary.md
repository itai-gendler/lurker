---
kind: primary
routes:
  web: Web
  client: Client API
  irc: IRC bouncer
steps:
- text: Incoming IRC activity or available engine backlog arrives.
  kind: condition
  entities: []
  contexts: &id001
    web:
      place: web::personal::channel
    client:
      place: client-api::personal
    irc:
      place: irc-bouncer::personal
  unattended: true
- text: Accepted incoming IRC activity recorded/delivered unattended
  kind: product
  entities:
  - entity: message
    effect: creates
    facts:
    - Sender
    - Content
    - Kind
    - Time
    - Self attribution
    - Upstream identity
    - Reply context
    - Highlight information
    - Ignore information
    - Encryption indication
    to: Recorded
  contexts: *id001
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
  target: server/services/ircConnection.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Receive messages

## Trigger

Incoming IRC activity or available engine backlog arrives.

## Outcome

Accepted incoming IRC activity recorded/delivered unattended

Incoming accepted conversation content is recorded with upstream or receive time and ignore/highlight/reply annotations. App clients receive the recorded representation; bouncer live delivery follows filtered raw IRC relay.

## Edge cases

- Self echo can be adopted when supported; local self recording is used on the no-echo path. Engine replay deduplicates available backlog but cannot promise complete recovery across a continuity gap.
