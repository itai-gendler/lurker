---
kind: path
routes:
  irc: IRC bouncer
steps:
- text: The User queries the current IRC read marker without supplying an advancing timestamp.
  kind: actor
  entities: []
  contexts: &id002
    irc:
      place: irc-bouncer::personal
  actor: user
- text: For the selected supported buffer, query returns current shared marker without advancing it
  kind: product
  entities:
  - entity: channel
    effect: reads
    facts: &id001
    - Read boundary
  - entity: direct-message
    effect: reads
    facts: *id001
  contexts: *id002
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
  target: server/db/bufferReads.ts
- kind: code
  role: implementation
  target: server/services/bouncer.ts
---

# Mark read marker query

## Trigger

The User queries the current IRC read marker without supplying an advancing timestamp.

## Outcome

Query returns current shared marker without advancing it

Only the addressed channel or private-message marker is read or changed; server/system/DCC targets are excluded by the bouncer contract.
