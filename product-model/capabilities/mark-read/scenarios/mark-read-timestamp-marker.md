---
kind: path
routes:
  irc: IRC bouncer
steps:
- text: The User submits a supported timestamp read marker through the downstream attachment.
  kind: actor
  entities: []
  contexts: &id002
    irc:
      place: irc-bouncer::personal
  actor: user
- text: For the selected supported buffer, accepted timestamp marker advances shared boundary
  kind: product
  entities:
  - entity: channel
    effect: changes
    facts: &id001
    - Read boundary
    - Unread counts
  - entity: direct-message
    effect: changes
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

# Mark read timestamp marker

## Trigger

The User submits a supported timestamp read marker through the IRC client.

## Outcome

Accepted timestamp marker advances shared boundary

Only the addressed channel or private-message marker is read or changed; server/system/DCC targets are excluded by the bouncer contract.
